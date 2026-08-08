# Five-check auditor

A conversational auditor that walks five checks against any failing setup, scores each, identifies the deciding crack, and returns a call with owner and tripwire.

---

## What this auditor does

A stranger describes a failing setup they rely on. The auditor:

1. Walks five checks conversationally
2. Scores each check (1–5)
3. Proposes findings with the measurement that would confirm each
4. Identifies the top crack (the check that decides)
5. Returns a call (ship / ship-with-conditions / hold) with an owner on any condition
6. Sets a tripwire: a number, a danger line, and who watches it

---

## The five checks

| Check | What it tests |
|-------|---------------|
| **Unowned** | Does any part of the failure have no clear owner? |
| **Copies** | Are there duplicate or conflicting sources of truth? |
| **Room** | Is there space in the workflow for the fix to land? |
| **Stitch** | Do handoffs between components drop information? |
| **Ablation** | If you removed a piece, would anyone notice? |

---

## Worked example

### Specimen

Store FAQ bot that picks an answer from the help center

### Stakes

Shoppers get the wrong policy and leave the cart

### Standard line (how you know it's fixed)

The answer matches the shopper's real ask — not a nearby FAQ about the same product

### Real inputs

Short mobile questions with product names in the middle

### Failing sentences (from store help-desk chat logs)

```
how long do i have to return the Nova Buds after they ship
Nova Buds delivery says Friday — can i still cancel
refund for wrong size on the Trail Jacket, not a shipping question
```

### Check ratings

| Check | Score |
|-------|-------|
| Unowned | 4 |
| Copies | 2 |
| Room | 1 |
| Stitch | 2 |
| Ablation | 1 |

### Top crack

**Unowned** — this check decides.

### Call

Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

### Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## How to use this auditor

### Input format

Provide:

1. **What tool is broken** — name the failing setup
2. **What goes wrong if this never gets fixed** — the stakes
3. **How will you know it's fixed** — a clear pass check
4. **Three real failing inputs** — paste them verbatim

### Output format

The auditor returns:

1. **Check scores** — each of the five checks rated 1–5
2. **Findings** — what each score means, with the measurement that would confirm it
3. **Top crack** — which check decides
4. **Call** — ship / ship-with-conditions / hold, with owner on any condition
5. **Tripwire** — the number to watch, the danger line, and who escalates

---

## Acceptance criteria

- Auditor walks all five checks for a stranger's specimen
- Every finding names the measurement that would confirm it
- Each result includes a call with an owner on any condition
- Each result includes an alarm with a number, a danger line, and a watcher
- The builder's own audit (Store FAQ bot) is visible as the worked example

---

## Sample asks

A stranger might paste:

> "Our support chatbot keeps answering billing questions with product feature docs. Three examples: 'why was I charged twice for Pro plan', 'cancel my subscription before next billing', 'refund for the month I didn't use'. What's broken?"

The auditor walks the five checks, scores each, identifies the top crack, and returns a call with owner and tripwire — applying the same discipline shown in the Store FAQ bot worked example.
