# Related notes

This repository sits alongside other notes the author keeps. Most of those notes are private; this one is public because the patterns are general enough to be adopted by another engineer running comparable work.

---

## What is in this repository

The five notes that precede this one document operational practices that produced the Aletheia stack:

- `01-shipping-order.md` — when to ship the implementations before the paper.
- `02-fresh-context-review.md` — using a second AI instance for cold review.
- `03-memory-layers.md` — two-layer persistence across sessions.
- `04-hardening-pipeline.md` — eight phases for moving a repo from runnable to defensible.
- `05-format-emergence.md` — observations from the four-implementation convergence on the wire format.

Each note is short by intent. The patterns are documented; the philosophy is not.

---

## What is documented privately

The author keeps additional notes — on writing style, formatting choices, signature conventions — that govern how outputs are shaped at the prose surface. Those notes are not part of this public repository because they are too specific to one author and one situation to be useful as a public reference.

If you are an engineer adopting the patterns in this repo, the prose-surface choices in your own work should come from your own preferences, not from copying what is documented privately for one author.

---

## How this repo relates to the Aletheia stack

The Aletheia stack is the technical work: the position paper, the applied papers, the wire format specification, the four agent-economy reference implementations, the Rust crate, the Solidity contracts.

These notes are about *how* that work was done, not what it does.

The technical work stands on its own. A reader who never sees this repository can still evaluate the Aletheia stack on its merits. These notes are an optional sidebar for engineers who want to understand the workflow that produced it.

If the Aletheia stack does not stand on its own, no amount of process documentation rescues it. If the stack does stand on its own, this repository is a small additional artifact that may be useful to others.

---

## License

CC BY 4.0. Adapt freely with attribution.

---

## A note on adapting to your own situation

The patterns here are extracted from how *I* think and ship.

Another engineer adapting them will end up with different patterns. That is correct. The contract is the practice of extraction and application, not the specific patterns extracted.

The shape of the practices is portable. The contents are not.

If you are reading this with intent to adopt, do not copy. Extract from your own work, apply to your own situation, document, iterate.

---

Juan Cruz Maisú ♥
