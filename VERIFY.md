# Verifying the Store FAQ Bot Audit

This document confirms that the Five-check auditor surfaces the correct findings when a stranger runs the sample setup through `/play`.

---

## What to verify

When you paste the Store FAQ bot specimen into the auditor, confirm:

1. **The deciding check surfaces clearly.** The tool must identify "unowned" as the top crack — the check that decides whether this setup ships.

2. **A numeric measurement is demanded.** The auditor must not accept vague findings. For the unowned check, it should require a count or rate — for example, the number of tickets containing refund/return/cancel words that get answered with shipping content.

---

## Sample stranger run

Paste this into `/play`:

> I have a Store FAQ bot that picks an answer from the help center. Shoppers get the wrong policy and leave the cart. Here are three real failing inputs from store help-desk chat logs:
>
> - how long do i have to return the Nova Buds after they ship
> - Nova Buds delivery says Friday — can i still cancel
> - refund for wrong size on the Trail Jacket, not a shipping question
>
> The pass standard: The answer matches the shopper's real ask — not a nearby FAQ about the same product.

---

## Expected output

The auditor should return:

- **Scored checks** across all five dimensions
- **Top crack identified:** unowned (no part of the system treats refund/return/cancel words as a priority signal)
- **Severity story** walking through one of the specimen sentences and showing the wrong output
- **Call:** Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.
- **Tripwire with a number:** Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Verification checklist

| Check | Pass criteria |
|-------|---------------|
| Deciding check surfaces | Tool names "unowned" as the top crack |
| Numeric measurement demanded | Finding includes a specific count or threshold (e.g., "10 per day") |
| Call is actionable | Includes owner (engineering lead) and reopening condition |
| Tripwire is concrete | Names the metric, the danger line, and who watches it |

If all four pass, the auditor is working correctly for this specimen domain.
