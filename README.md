# Five-check auditor

**Worked example:** Store FAQ bot that picks an answer from the help center

---

## What this audits

Shoppers ask about refunds, but the FAQ bot answers with shipping times because it latched onto the product name. This auditor walks five checks to find where the setup breaks and whether it's safe to ship.

**Stakes if unfixed:** Shoppers get the wrong policy and leave the cart

**Pass standard:** The answer matches the shopper's real ask — not a nearby FAQ about the same product

---

## Verdict

**Hold.** No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

**Deciding check:** Unowned (scored 4/5 severity)

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## One-paste rebuild

Copy this block into a new conversation to run the Five-check auditor on your own failing setup:

```
I have a failing setup I need audited.

Setup: [describe what the tool is supposed to do]
Stakes: [what goes wrong if this never gets fixed]
Pass standard: [how you'll know it's fixed]

Real failing inputs:
1. [paste a real message where it fails]
2. [paste another]
3. [paste a third]

Source: [where those inputs came from]

Walk me through the five checks, propose findings with the measurement that would confirm each, then give me a scored audit with a severity story, a call (ship / ship-with-conditions / hold), and a tripwire.
```

---

## Sample asks

A stranger pastes their own failing setup for the auditor to score:

- "My support chatbot keeps answering billing questions with product feature descriptions. Three real failures: 'why was I charged twice for the Pro plan', 'cancel my subscription before next billing', 'refund for the month I didn't use'. Pulled from Zendesk last week. Walk the five checks."

- "Our internal knowledge-base search returns HR policy docs when people search for IT troubleshooting. Real inputs: 'reset my VPN password', 'laptop won't connect to wifi', 'how do I get admin access'. From IT helpdesk tickets. Give me the audit."

- "The appointment booking bot confirms the wrong service type — customers book 'haircut' and get scheduled for 'color consultation'. Three failures from last month's logs. Run your five checks and tell me if we ship."

---

## Files in this repo

| File | Purpose |
|------|---------|
| `charter.md` | Full audit grounded in the Store FAQ bot specimen |
| `METHOD.md` | The five-check framework (PRISM) |
| `VERIFY.md` | How a stranger verifies the auditor works |

<!-- educationpals-build-verified -->
