# Audit Memory System

This documents how to read and write per-product audit history so Hermes can track UX health over time.

---

## Overview

Every completed audit writes a JSON record to:
```
~/audits/history/[product-slug].json
```

On the next audit of the same product, the agent reads this file first and uses it to:
1. Identify which previous findings were fixed vs. still present
2. Show a score trend (was the product improving or regressing?)
3. Avoid re-explaining findings the team already knows about

---

## Step 0 Addition — Check Audit History Before Starting

**At the start of every audit, after Step 0.4 (product understanding), run this before any checklist work:**

```bash
python3 - << 'PY'
import json, os, sys

slug = sys.argv[1] if len(sys.argv) > 1 else "UNKNOWN"
history_path = f"/home/brew/audits/history/{slug}.json"

if not os.path.exists(history_path):
    print(json.dumps({"first_audit": True, "message": f"No history found for {slug} — this is the first audit."}))
else:
    with open(history_path) as f:
        data = json.load(f)
    
    audits = data.get("audits", [])
    if audits:
        last = audits[-1]
        open_findings = [f for f in last.get("findings", []) if f.get("status") != "fixed"]
        print(json.dumps({
            "first_audit": False,
            "last_audit_date": last["date"],
            "last_score": last.get("score"),
            "audit_count": len(audits),
            "previously_open_findings": open_findings,
            "message": f"Found {len(audits)} previous audit(s). Last score: {last.get('score', 'N/A')}. {len(open_findings)} findings still open from last audit."
        }, indent=2))
PY
```

Replace `UNKNOWN` with the product slug (e.g., `stylemeup`, `skechers-in`).

**If a history file exists**, include this section at the top of your brief (Step 0.4):
```
## Audit History Context
Previous audits: [N]
Last audit: [date] — Score: [X/10]
Previously filed findings still open: [list finding IDs + titles]
Note: Check explicitly whether each of the above was fixed in this audit.
```

**If no history file**, proceed normally — this is a fresh baseline.

---

## How to Check if a Previous Finding Was Fixed

For each previously open finding, during your Pass 1 and Pass 2:
- If you **cannot reproduce** the issue → mark it "fixed"
- If you **can reproduce** it → it's still open, note it as "persistent"
- If the issue **changed** (e.g., was P1, now addressed but partially) → "partially fixed"

Report these in the executive summary:
> "Previously filed: FLOW-001 (paywall before value) — **still open**. TRUST-003 (face privacy disclosure) — **fixed** (disclosure now appears at upload step)."

---

## Step 6 Addition — Write Audit History After Completing

After writing the markdown report and before generating the PDF, write the history record:

```bash
python3 - << 'PY'
import json, os, datetime

# ── FILL THESE IN ──────────────────────────────────────────
SLUG = "product-slug"              # e.g. "stylemeup"
PRODUCT_NAME = "Product Name"      # e.g. "StyleMeUp"
PRODUCT_TYPE = "mobile app"        # e.g. "mobile app", "website", "SaaS app"
DOMAIN = "fashion/ai"              # e.g. "ecommerce", "fintech", "saas-b2b"
SCORE = 7.5                        # overall UX score out of 10

# List every finding. Status: "open" | "fixed" | "partially_fixed" | "new" | "persistent"
FINDINGS = [
    {"id": "FLOW-001", "priority": "P1", "status": "persistent", "title": "Paywall before first value"},
    {"id": "TRUST-003", "priority": "P1", "status": "fixed",     "title": "No face privacy disclosure"},
    {"id": "NOTIFY-001","priority": "P2", "status": "new",       "title": "Offline retry broken"},
]
# ───────────────────────────────────────────────────────────

history_path = f"/home/brew/audits/history/{SLUG}.json"
today = datetime.date.today().isoformat()

# Load existing or create new
if os.path.exists(history_path):
    with open(history_path) as f:
        data = json.load(f)
else:
    data = {"slug": SLUG, "product_name": PRODUCT_NAME, "product_type": PRODUCT_TYPE, "domain": DOMAIN, "audits": []}

# Add this audit
data["audits"].append({
    "date": today,
    "score": SCORE,
    "findings": FINDINGS,
    "report_path": f"/home/brew/audits/{SLUG}-{today}.md"
})

# Update metadata
data["product_name"] = PRODUCT_NAME
data["product_type"] = PRODUCT_TYPE
data["domain"] = DOMAIN
data["last_audit"] = today
data["last_score"] = SCORE

os.makedirs("/home/brew/audits/history", exist_ok=True)
with open(history_path, "w") as f:
    json.dump(data, f, indent=2)

print(f"History written to {history_path}")
print(f"Total audits on record: {len(data['audits'])}")

# Print score trend if multiple audits
if len(data["audits"]) >= 2:
    scores = [a["score"] for a in data["audits"] if a.get("score")]
    if len(scores) >= 2:
        trend = scores[-1] - scores[-2]
        direction = "↑" if trend > 0 else "↓" if trend < 0 else "→"
        print(f"Score trend: {scores[-2]} → {scores[-1]} ({direction}{abs(trend):.1f})")
PY
```

---

## Score Trend in Executive Summary

If the history file has 2+ audits, add this line to the executive summary:

> "UX score: **7.5/10** (was 6.2 in June — ↑1.3 improvement)"

If this is the first audit:
> "UX score: **7.5/10** (baseline — first audit)"

---

## History File Format Reference

```json
{
  "slug": "stylemeup",
  "product_name": "StyleMeUp",
  "product_type": "mobile app",
  "domain": "fashion/ai",
  "last_audit": "2026-06-04",
  "last_score": 7.5,
  "audits": [
    {
      "date": "2026-06-04",
      "score": 7.5,
      "report_path": "/home/brew/audits/stylemeup-2026-06-04.md",
      "findings": [
        {"id": "FLOW-001", "priority": "P1", "status": "persistent", "title": "Paywall before first value"},
        {"id": "TRUST-003", "priority": "P1", "status": "fixed", "title": "No face privacy disclosure"}
      ]
    }
  ]
}
```

Statuses:
- `new` — first time this finding appears
- `persistent` — was open in previous audit, still open
- `fixed` — was open, now resolved
- `partially_fixed` — addressed but not fully resolved
- `open` — use for first-audit findings
