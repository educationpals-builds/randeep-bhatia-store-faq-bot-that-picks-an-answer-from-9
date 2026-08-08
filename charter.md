# Audit: Store FAQ bot that picks an answer from the help center

## Specimen under review

**Tool:** Store FAQ bot that picks an answer from the help center

**Stakes if unfixed:** Shoppers get the wrong policy and leave the cart

**Standard for pass:** The answer matches the shopper's real ask — not a nearby FAQ about the same product

## Real inputs

**Usage pattern:** Short mobile questions with product names in the middle

**Source:** Store help-desk chat logs

### Pasted failing messages

```
how long do i have to return the Nova Buds after they ship
Nova Buds delivery says Friday — can i still cancel
refund for wrong size on the Trail Jacket, not a shipping question
```

---

## Five-check findings

| Check | Rating | Notes |
|-------|--------|-------|
| Unowned | 4 | High severity — no component owns refund/return/cancel intent |
| Copies | 2 | Some duplication in FAQ matching logic |
| Room | 1 | Minimal headroom for edge cases |
| Stitch | 2 | Weak handoff between product-name detection and intent classification |
| Ablation | 1 | Removing product-name matching breaks routing entirely |

---

## Deciding check

**Top crack:** Unowned

No part of the system currently owns the refund/return/cancel signal. When a shopper types "refund for wrong size on the Trail Jacket, not a shipping question," the bot latches onto "Trail Jacket" and returns shipping FAQs — because nothing in the pipeline prioritizes the explicit refund words over the product name match.

---

## Call

**Verdict:** Hold

Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

| Metric | Danger line | Watcher |
|--------|-------------|---------|
| Tickets with refund/return/cancel word answered with shipping content | >10 per day during sale week | CX manager escalates to engineering |

---

## Summary

This audit found the Store FAQ bot fails the **Unowned** check most severely. The system has no dedicated handler for refund/return/cancel intent, so product-name matching dominates routing even when the shopper explicitly states their question is not about shipping. The call is **Hold** until engineering adds a priority signal for these keywords and the three specimen sentences route correctly.
