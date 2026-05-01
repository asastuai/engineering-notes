# Working Method

### How an independent researcher and an AI collaborator built a research family of papers, a verification stack, and a wire format in eight months

By [Juan Cruz Maisú](https://github.com/asastuai). Buenos Aires.

---

## What this is

A small body of artifacts documenting the working method that produced:

- A position paper (Proof-of-Context v0.6) and two applied papers (v0.1 Inference, v0.1 Agent Economy Infrastructure, v0.1 Agent Service Settlement).
- Five reference implementations across Rust, JavaScript, TypeScript, Solidity.
- A versioned wire-format specification that emerged from running the same primitive through four independent consumer surfaces.
- A multi-phase hardening pipeline that took the four "almost-oneshotted" repositories from no-tests-and-aspirational-claims to forty-three integration tests passing, signed Ed25519 attestations on every paid endpoint, and an honest README per repo.

The method is the artifact.

The papers are downstream of the method. The implementations are downstream of the method. The wire format is downstream of the method. None of them would have shaped the way they did without the method shaping them.

This repository documents the method.

---

## How to read this

Six short documents in order.

1. [`01-the-inversion.md`](./01-the-inversion.md) — primitive-after-paper inversion. Why the implementations preceded the paper, and what that order earns.
2. [`02-the-adversarial-review.md`](./02-the-adversarial-review.md) — the protocol for passing work to a second AI instance for fresh-context review, and the Q-terror exercise.
3. [`03-the-memory-protocol.md`](./03-the-memory-protocol.md) — two-layer persistence (auto-memory per project + engram cross-project). What gets saved. What does not.
4. [`04-the-hardening-pipeline.md`](./04-the-hardening-pipeline.md) — the eight-phase pipeline that takes a freshly-written repository to outreach-defensible state.
5. [`05-the-wire-format-convergence.md`](./05-the-wire-format-convergence.md) — how four independent implementations converged on the same on-wire format and what the convergence proves.
6. [`06-the-companion-protocols.md`](./06-the-companion-protocols.md) — links to the sister contracts: voice channel, artisanal glyphs alphabet.

---

## ◊ What this is not

It is not a methodology framework. Methodology frameworks claim universality.

It is not a guide to working with AI. Guides to working with AI prescribe.

It is not a manifesto. Manifestos demand adoption.

It is one author's documented practice, with worked examples, that other authors can adapt or reject. The contract is the practice. The patterns are downstream.

If you are an independent researcher working with AI tools and want a starting point, the value is in the *moves*, not in copying the artifacts they produced.

---

## ❖ Companion repositories

This repository is one of two that document the method's surface.

- [**voice-as-channel**](https://github.com/asastuai/voice-as-channel) — how the AI was taught to write in the author's voice. The communication-channel layer.
- **working-method** — *(this repository)* — the research-and-build practice itself. The work-shape layer.

The two are read together. The voice channel without the method produces well-styled emptiness. The method without the voice produces work that does not feel authored. Both are needed.

---

## License

CC BY 4.0. Use it. Adapt it. Credit the source.

---

Juan Cruz Maisú ♥
