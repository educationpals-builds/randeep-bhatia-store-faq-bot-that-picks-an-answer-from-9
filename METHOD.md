# The Five-Check Method

This document explains the five checks that power the auditor. Each check corresponds to one letter in **PRISM**.

---

## P — Partition the Space

Before anything else, confirm the system divides incoming requests into distinct buckets. A store FAQ bot handling refunds, shipping, and cancellations needs separate partitions for each intent—not one giant "product questions" bucket.

**What to measure:** Count how many top-level intent categories exist. If a single category handles more than 40% of traffic, the partition is too coarse.

**Anti-pattern (collapse-to-monochrome):** Treating every question as "product inquiry" because the product name appears in the message. When a shopper asks "how long do i have to return the Nova Buds after they ship," the system must see *return* as the partition—not *Nova Buds*.

---

## R — Run in Parallel

Each partition should run its own detection logic simultaneously, not sequentially. If the system checks "Is this about shipping?" first and stops there, it never asks "Is this about refunds?"

**What to measure:** Trace one ambiguous input through the pipeline. Count how many intent classifiers fire before a decision is made. If only one fires, parallel coverage is missing.

**Anti-pattern (collapse-to-monochrome):** A single classifier that picks the first plausible match. "Nova Buds delivery says Friday — can i still cancel" triggers shipping because *delivery* appears before *cancel*.

---

## I — Individuate the Pattern

Each check must have its own signature—specific words, phrases, or structures that belong to it and not to neighbors. Refund questions have patterns ("return," "refund," "money back") that shipping questions lack.

**What to measure:** List the trigger words for each partition. If two partitions share more than half their triggers, they aren't individuated.

**Anti-pattern (collapse-to-monochrome):** Relying on product names as the primary signal. "Nova Buds" appears in refund questions, shipping questions, and cancellation questions—it individuates nothing.

---

## S — Stitch the Spectra

When multiple signals fire, the system must combine them with explicit priority rules. A message mentioning both "delivery" and "refund" needs a stitching rule that says which wins.

**What to measure:** Find a message that triggers two partitions. Document the rule that resolves the tie. If no rule exists, stitching is absent.

**Anti-pattern (collapse-to-monochrome):** Letting the first match win by default. "refund for wrong size on the Trail Jacket, not a shipping question" gets routed to shipping because the system saw "Trail Jacket" and stopped thinking.

---

## M — Map What Each Head Sees

After classification, verify that each partition's response logic actually addresses the classified intent. A refund partition that returns shipping FAQs has a broken map.

**What to measure:** For each partition, sample five classified inputs and check whether the returned answer matches the intent. If more than one answer mismatches, the map is broken.

**Anti-pattern (collapse-to-monochrome):** One answer pool for all partitions. The system classifies correctly but pulls from a single FAQ list sorted by product name, so "Nova Buds" questions all get the same answer regardless of intent.

---

## The Collapse-to-Monochrome Anti-Pattern

Every check above can fail the same way: the system reduces a multi-dimensional question to a single dimension (usually the product name) and ignores everything else.

A store FAQ bot that latches onto "Nova Buds" and ignores "return," "cancel," or "refund" has collapsed to monochrome. The fix is never "try harder"—it's adding explicit checks for the dimensions the system currently ignores.

When you audit a failing setup, look for monochrome collapse first. It explains most routing failures in systems that "sort of work" but miss obvious cases.
