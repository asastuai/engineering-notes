# The Wire Format Convergence

Four implementations. One author. The same shape.

The convergence is a small empirical fact about the working method. It also happens to be the central conceptual contribution of one of the papers. This document explains what the convergence was, what it earned, and why it is more interesting than it sounds.

---

## ◊ What converged

In the course of building five Proof-of-Context-related repositories, i implemented the on-wire shape of an attestation four separate times.

Once in JavaScript, in `BaseOracle/src/utils/poc.js`. The repo's job is to serve paid market data. The attestation rides on the response payload of every paid endpoint.

Once in JavaScript, in `TrustLayer/src/utils/poc.js`. The repo's job is to aggregate per-agent reputation. Different repo, different surface, different freshness types being emitted.

Once in TypeScript, in `vigil/packages/core/src/poc.ts`. The repo's job is to compute DeFi risk signals and serve them via x402. TypeScript, different language, different dependency graph.

Once in TypeScript, in `payclaw/packages/sdk/src/poc.ts`. The repo's job is the agent wallet — a *consumer* of attestations, not a producer. The verifier runs there. The shape it expects to verify is what it expects.

Plus a Rust reference crate, `proof-of-context-impl`, that defines the types in a fifth language.

Five implementations. Four authored by the same person. One produced earlier as the reference crate.

---

## What was the same

Every implementation produced an `_poc` block on the wire with the same fields:

```
{
  version, freshness_type, source_id, endpoint, timestamp,
  freshness_horizon_seconds, payload_hash, signature, public_key,
  anchors: { server_timestamp, block_height, drand_round },
  scope_disclaimer
}
```

The fields appeared in the same order. They had the same names. They had the same semantics. They were signed over the same canonical message — a sorted-keys JSON of the signing-relevant subset, encoded as UTF-8, hashed with SHA-256, signed with Ed25519.

A producer in one language could sign an attestation. A consumer in another language could verify the signature. They did, in tests. They still do.

---

## ❖ Why this is more interesting than it sounds

i wrote the four implementations. Same author, same head, same set of design pressures.

The naive reading: "of course they converged. The same person wrote them."

That reading is partly correct. Self-coordination is a real factor. The author did not consciously arrive at five distinct designs and then merge them.

But the convergence has structure that self-coordination alone does not produce.

### The convergence covered fields the author did not initially intend to share

The first implementation (BaseOracle) emitted only `f_i` (input freshness). It did not need a `freshness_type` field at all. The field was added later when the second implementation (TrustLayer) needed multiple types.

When the author went back and added `freshness_type` to BaseOracle, the choice of putting it as the second field of the `_poc` block (after `version`) was made independently for each implementation. The implementations were not yet sharing code. The author was not yet looking at all four side by side.

The choice of position — second field, not last, not buried — was the same choice made twice.

The convergence is that two independent applications of the same author's judgment produce the same answer. That is not nothing. It is a signal that the underlying design space has structure that the author's judgment is detecting, not inventing.

### The convergence covered field names

`freshness_horizon_seconds`, not `expiry`, not `ttl`, not `max_age`, not `valid_until_epoch`.

The default vocabulary in the JavaScript ecosystem leans toward `ttl` or `maxAge`. The default vocabulary in TypeScript leans the same way. The Rust reference crate, written first, used `freshness_horizon_seconds`. The two JavaScript implementations, written later, both reached for the same name.

The reaching is the signal.

### The convergence covered exclusion as much as inclusion

The signing message intentionally excludes the `anchors` block. This is a non-obvious choice. A naive design would include anchors in the signing surface to make them tamper-evident.

The reason for the exclusion: triple-anchor values can differ between issuance and verification (caches, retries, partial fetches). Including them in the signing surface would invalidate every replay-with-cached-anchor scenario without protocol benefit.

i made this exclusion choice in BaseOracle first. By the time i was implementing PayClaw's verifier, i had to recreate the same exclusion choice on the verification side. The choice held.

If the convergence were just self-coordination, the exclusion would have been a flat-out mistake i replicated. It is not a mistake. It is the right answer to a sub-problem the design space presents. The convergence happened because the right answer is unique enough that two implementations of the same author's judgment land on it.

---

## What the convergence proves

It proves something modest. Independently-implemented surfaces of a primitive, when designed by an author who has internalized the primitive's constraints, converge on the same on-wire shape.

This is empirical evidence for one specific claim made in the applied paper: that the wire format that emerged is *interop-able infrastructure*, not a hypothesis. The convergence is the artifact's evidence-of-shape.

If the same implementations had been written by four different authors with no coordination, the convergence would prove a much stronger claim — that the design space *imposes* the format. With one author, the claim is weaker but still meaningful: the design space *suggests* the format strongly enough that one mind, working independently, lands on it four times.

The next iteration of this experiment, if it happens, would be different authors writing the implementations. That experiment is open.

---

## ※ A note on what this means for the paper

The applied paper #2 ("PoC for Agent Economy Infrastructure") makes the convergence its central conceptual contribution. The paper documents what already happened, names what already converged, and proposes the result as a working specification.

The paper does not claim that the author *invented* the wire format. The paper claims that the wire format *emerged*, and that the author was the surface on which the emergence first became visible.

This framing matters. A paper that claims invention is making a contribution claim that other authors can dispute. A paper that documents emergence is making a description claim that other authors can replicate.

The replication is the next research surface. Other implementations by other authors should land on the same shape. If they do, the wire format is real. If they do not, the wire format was self-coordination after all.

Time will tell.

---

## ◊ How to apply the convergence pattern in your own work

If you are an independent researcher building primitives in the agent economy or in any space with multiple consumer surfaces:

- **Implement the primitive at least three times in different surfaces before writing the paper.** The convergence makes the paper's job easier. The divergence (if it happens) shows you that your primitive is not yet stable.
- **Do not look at the implementations side by side until each is done.** Looking at the previous implementation while writing the next one is self-coordination. The convergence claim relies on independence between iterations.
- **Document what was the same and what was different.** The differences are as informative as the similarities. Both teach the design space.
- **Treat the convergent format as evidence, not invention.** The paper that frames a convergent shape as discovery is honest. The paper that frames it as invention overstates.

The convergence is the working method's reward for the inversion of `01-the-inversion.md`. The implementations preceded the paper, and the paper now has empirical anchoring it would not otherwise have had.

---

Juan Cruz Maisú ♥
