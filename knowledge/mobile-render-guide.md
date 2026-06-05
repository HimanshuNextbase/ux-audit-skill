# Mobile App Rendering Guide

The audit server cannot run a device emulator. BUT — it CAN run a local dev server and use browser tools to screenshot the app if a web-renderable build is possible. **Always attempt to render the app first.** Screenshots from code give real visual evidence — spacing, typography, colour, layout — that code alone cannot.

**PRIORITY ORDER — try each in sequence, stop at the first that works:**

---

## Attempt 1 — Expo Web (React Native / Expo apps)

Most Expo apps can run in a browser even without explicit web support. Run this sequence:

```bash
# 1. Detect framework
cat package.json | python3 -c "import sys,json; d=json.load(sys.stdin); deps={**d.get('dependencies',{}),**d.get('devDependencies',{})}; print('expo' if 'expo' in deps else 'rn-bare' if 'react-native' in deps else 'other')"

# 2. Check if web already configured
python3 -c "
import json
try:
    with open('app.json') as f: d=json.load(f)
    platforms = d.get('expo',{}).get('platforms', [])
    print('web_configured:', 'web' in platforms)
    print('platforms:', platforms)
except: print('web_configured: unknown')
"

# 3. If web NOT configured — add it temporarily
python3 -c "
import json
with open('app.json') as f: d=json.load(f)
expo = d.setdefault('expo', {})
platforms = expo.get('platforms', ['ios', 'android'])
if 'web' not in platforms:
    expo['platforms'] = platforms + ['web']
    with open('app.json', 'w') as f: json.dump(d, f, indent=2)
    print('Added web platform to app.json')
else:
    print('Web already configured')
"

# 4. Install web peer deps (fast — usually cached)
npx expo install @expo/webpack-config react-native-web react-dom 2>&1 | tail -5

# 5. Start Expo web server in background
npx expo start --web --port 19006 --no-dev --https false 2>&1 &
EXPO_PID=$!

# 6. Wait for server to be ready (up to 45s)
for i in $(seq 1 45); do
  curl -s http://localhost:19006 > /dev/null 2>&1 && echo "Server ready after ${i}s" && break
  sleep 1
done
```

Then use browser tools:
```
browser_navigate("http://localhost:19006")
```
Resize viewport to 390px width (mobile), run the settled-check, then screenshot.

**Navigate through the app's key screens** by clicking nav items, tab bar buttons, and primary CTAs — screenshot each one. Cover: home, onboarding (if reachable), core task, empty state (clear local storage to force it), a form.

After the audit, restore `app.json` if you modified it:
```bash
git checkout app.json 2>/dev/null || true
kill $EXPO_PID 2>/dev/null || true
```

**What works in Expo Web:** standard RN components (`View`, `Text`, `TextInput`, `ScrollView`, `FlatList`, `Image`, `TouchableOpacity`, `Pressable`, most navigation). **What breaks:** native modules (`react-native-camera`, `react-native-maps`, Bluetooth, biometrics, etc.) — these crash the web bundle. If the build fails due to a native module, skip that module's screens and note "Native module [X] not renderable on web."

---

## Attempt 2 — React Native Web manual setup (bare RN without Expo)

If there's no Expo but standard React Native:

```bash
# Install react-native-web + bundler
npm install react-native-web react-dom
npm install --save-dev @vitejs/plugin-react vite

# Create a minimal vite config
cat > vite.config.js << 'EOF'
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
export default defineConfig({
  plugins: [react()],
  resolve: { alias: { 'react-native': 'react-native-web' } },
  define: { __DEV__: false },
})
EOF

# Create a minimal web entry
cat > index.html << 'EOF'
<!DOCTYPE html><html><body><div id="root"></div><script type="module" src="/src/index.web.js"></script></body></html>
EOF

# Find the app entry point and create web entry
ENTRY=$(cat package.json | python3 -c "import sys,json; d=json.load(sys.stdin); print(d.get('main','index.js'))")
cat > src/index.web.js << EOF
import { AppRegistry } from 'react-native'
import App from './$ENTRY'
AppRegistry.registerComponent('App', () => App)
AppRegistry.runApplication('App', { rootTag: document.getElementById('root') })
EOF

npx vite --port 19007 &
sleep 10
browser_navigate("http://localhost:19007")
```

---

## Attempt 3 — Flutter Web

```bash
# Check if Flutter web target exists
ls web/index.html 2>/dev/null && echo "web target exists" || echo "no web target"

# If exists:
flutter build web --release 2>&1 | tail -10
cd build/web && python3 -m http.server 19008 &
sleep 5
# browser_navigate("http://localhost:19008")

# If web target doesn't exist — add it:
flutter create --platforms web . 2>&1 | tail -5
flutter build web 2>&1 | tail -10
```

---

## Attempt 4 — Storybook (component-level screenshots)

If the app has Storybook configured (`@storybook/react-native`, `.storybook/` directory):

```bash
ls .storybook/ 2>/dev/null && echo "Storybook found"
npx storybook --port 6006 &
sleep 15
# browser_navigate("http://localhost:6006")
```

Screenshot each story — especially loading, error, empty, and form states that are hard to trigger in the full app. Label each screenshot with the component and state name.

---

## Attempt 5 — Ask for screenshots (last resort)

Only if ALL web render attempts fail (native-only modules blocking every attempt):

> "The app uses native modules that can't run in a browser ([list the failing modules]). The code audit is running now. To complete the visual layer, please share screenshots from your device or simulator of: home screen, onboarding, core task, empty state, error state, a form."

Run Lane B immediately without waiting. Combine with screenshots when they arrive.

---

## Rendering fidelity note (always add to report header)

Always add a one-line note at the top of the report stating how the visual audit was done:
- "Visual audit: Expo Web build at 390px — some native components replaced with web equivalents"
- "Visual audit: Storybook component screenshots — full-app flow not captured"
- "Visual audit: User-provided device screenshots"
- "Visual audit: Not possible — native-only modules blocked all render attempts; code analysis only"
