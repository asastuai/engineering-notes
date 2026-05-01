# Engineering Notes

Practical notes on the workflow that produced the Aletheia stack: research papers, reference implementations, wire format specification, on-chain primitives, integration tests.

The goal of this repository is to document, in operational terms, the engineering practices that worked in this specific situation. Not as a method-with-a-capital-M; as a working set of habits, with worked examples, that another engineer can adapt.

By [Juan Cruz Maisú](https://github.com/asastuai). Buenos Aires.

---

## What you will find here

Six short documents.

1. [`01-shipping-order.md`](./01-shipping-order.md) — why the implementations were shipped before the paper was written, and what that order earned in this specific case.
2. [`02-fresh-context-review.md`](./02-fresh-context-review.md) — using a second AI instance for cold-context review, with the question set and the pre-mortem exercise.
3. [`03-memory-layers.md`](./03-memory-layers.md) — two-layer persistence (per-project auto-memory + cross-project engram). What the layers contain. What they do not.
4. [`04-hardening-pipeline.md`](./04-hardening-pipeline.md) — eight phases applied to four repositories that started in an under-tested, under-documented state and ended outreach-defensible.
5. [`05-format-emergence.md`](./05-format-emergence.md) — observations on how four reference implementations of the same primitive converged on the same on-wire format, and what that convergence does and does not prove.
6. [`06-related-notes.md`](./06-related-notes.md) — how this repo relates to other notes the author keeps.

---

## What this is not

These are notes, not a methodology. The word "method" or "framework" is intentionally avoided in the surface language because what is documented here is one situation, not a system.

These are not guides. Guides prescribe; these notes describe what worked here.

If you are an engineer or researcher running comparable work and want a starting point, the value is in the worked examples. The exact patterns are specific to one author and one stack.

---

## License

CC BY 4.0. Use it. Adapt it. Credit the source.

---

Juan Cruz Maisú ♥
