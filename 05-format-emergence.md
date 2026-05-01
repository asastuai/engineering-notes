# Format emergence

Four implementations. One author. The same shape on the wire.

This note describes what was observed across the four implementations of the Proof-of-Context wire format, what the observation supports, and what it explicitly does not.

---

## What was observed

In the course of building the Aletheia stack, I implemented the on-wire shape of a PoC attestation four separate times.

Once in JavaScript, in `BaseOracle/src/utils/poc.js`. The repo serves paid market data over x402; the attestation rides on every paid response.

Once in JavaScript, in `TrustLayer/src/utils/poc.js`. The repo aggregates per-agent reputation from four services. The same primitive, but different freshness types being emitted.

Once in TypeScript, in `vigil/packages/core/src/poc.ts`. The repo computes DeFi risk signals served via x402.

Once in TypeScript, in `payclaw/packages/sdk/src/poc.ts`. The repo's job is the agent wallet — a *consumer* of attestations, not a producer.

A fifth implementation in Rust, `proof-of-context-impl`, defines the types in a fifth language and was authored earlier as a reference crate.

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

Same field order. Same semantics. Same canonical signing message — sorted-keys JSON of the signing-relevant subset, encoded as UTF-8, hashed with SHA-256, signed with Ed25519.

A producer in one language could sign an attestation. A consumer in another language could verify the signature. They did, in tests. They still do.

---

## What this observation supports

The observation supports a calibrated claim: **independent surfaces of the same primitive, when implemented by an author who has internalized the constraints, converge on the same on-wire shape**.

The convergence is not free. The author wrote each implementation without copying code from the previous one. The choices that converged — field naming, field ordering, the deliberate exclusion of the anchors block from the signing surface — were made independently each time.

In the v0.1 spec language, this is described as *intra-author consistency under shared constraints*.

---

## What this observation does NOT support

The convergence does **not** demonstrate that the wire format's shape is *necessary* — that any independent author working from the spec alone would arrive at the same shape.

A naive reading of the convergence as "evidence the format is structurally tight" overreaches. Self-coordination is a real factor. The author had the spec in mind while writing each implementation; the convergence is partly a consequence of that internalization, not solely a consequence of the spec being narrow enough to permit only one shape.

The stronger claim — that an independent author would converge — requires a replication experiment with a second author. That experiment has not happened. It is identified as future work in the v0.1 spec and in the agent-economy paper.

---

## Where the observation is informative

The convergence is more interesting than naive self-coordination would predict for two specific reasons.

### It covered fields the author did not initially intend to share

The first implementation (BaseOracle) emitted only `f_i` (input freshness). It did not need a `freshness_type` field at all. The field was added later when the second implementation (TrustLayer) needed multiple types.

When the field was added back to BaseOracle, the choice of putting it as the second field of the `_poc` block (after `version`) was made independently of how the same choice had been made in TrustLayer. The implementations were not yet sharing code. The author was not yet looking at all four side by side.

The choice of position — second field, not last, not buried — was the same choice made twice without coordination. That is information about the design space, not just about author preference.

### It covered exclusion as much as inclusion

The signing message intentionally excludes the `anchors` block. This is a non-obvious choice. A naive design would include anchors in the signing surface to make them tamper-evident.

The reason for the exclusion: triple-anchor values can differ between issuance and verification (caches, retries, partial fetches). Including them in the signing surface would invalidate every replay-with-cached-anchor scenario without protocol benefit.

I made this exclusion choice in BaseOracle first. By the time I implemented PayClaw's verifier, the same exclusion choice had to be recreated on the verification side. The choice held.

If the convergence were just self-coordination at the surface, an exclusion that costs nothing and looks defensive in the abstract would have been included in some implementations and not others. The fact that it was made consistently is a property of the underlying design space, not just of author preference.

---

## Implications for use of the wire format

The current paper supports publishing the format as a stable contract for adoption by new integrators. Intra-author consistency is sufficient for that purpose: the contract holds, integrators can build against it.

Independent-author convergence would be required to claim that the format's shape is *necessary* rather than *one specific way of doing it*. The current observation does not support that stronger claim. The replication experiment is open.

---

## What this earns from the work

The wire format spec's authority comes from the convergence and from the worked implementations behind it. A spec without implementations would be hypothesis. A spec with one implementation would be illustration. A spec with four implementations, all independent, all producing byte-identical hashes — is a contract that already holds, even if the strength of the convergence claim is calibrated as documented above.

The next experiment in this line is one or more independent authors implementing the spec from scratch. If they converge, the format's shape is necessary. If they do not, what diverges is informative about the spec's tightness.

Either result advances the work.

---

Juan Cruz Maisú ♥
