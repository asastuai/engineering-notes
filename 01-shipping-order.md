# Shipping order: implementations before the paper

In this project, the implementations were shipped before the framework paper was written. The paper came after, drawing on the implementations as evidence rather than proposing them as future work.

This note explains the order, what it earned in this specific case, and where it does not work.

---

## What the order looks like

Five repositories were built first: a pay-per-query data layer, a reputation aggregator, a perp DEX with planned settlement gating, an agent wallet with a verifier, and a Rust crate with the primitive's types. Each repository accumulated design pressure over weeks of iteration. The first version of the data layer's response shape was wrong. The second was partially wrong. The third worked. Each iteration removed an assumption that the paper would otherwise have inherited.

By the time the paper was drafted, the framework's claims pointed at real choices in real code. The four freshness types were not abstract decompositions of staleness; they were the four things that turned out to need separate enforcement on different surfaces.

---

## What it earned in this case

Three concrete things, narrowly scoped to this project.

### Empirical anchoring

Every claim in the v0.6 framework paper points at a specific choice in a specific implementation. A reviewer can clone the repositories and verify the claim against the code. The chain of evidence is short.

### Pre-review by reality

The implementations had absorbed dozens of design pressures before the paper was written. The paper inherited none of them; the implementations had taken those hits already.

### Convergence as observation, not hypothesis

Four implementations of the same primitive converged on the same wire format (see `05-format-emergence.md`). The paper documents the convergence as something already happening. A paper proposing the same shape without the implementations would be hypothesis. With the implementations behind it, it is observation.

---

## Where this does not apply

Two cases.

### When the primitive is genuinely novel

If you are inventing something the world has never seen, building five implementations before any paper sees the light is not feasible. You have to formalize before you can replicate. This shipping order works when the primitive is *findable* in the existing solution space, where the paper's job is to name what is converging.

### When the implementations would be too expensive

Some primitives require months of engineering per implementation. Five of those is a multi-year commitment. This order works because each of the five repositories took weeks to a couple of months, not years.

If the primitive's natural implementation cost is high, the conventional paper-first order is correct.

---

## Why this happened in this specific situation

The order was not strategic. It was what was possible.

There was no academic affiliation, no co-authors, no reviewer pool to address. The standard incentives that produce paper-first order were not present. What was present was time, AI collaboration, and a willingness to ship public repositories before any paper existed. That setup made the order possible.

A traditional research career setup would have produced a different sequence. This is worth saying because the order is not a discovery — it is what an independent practitioner does when the conventional gates are not in the way.

---

## How to apply if you are in a similar situation

A practical check before writing a paper proposing a new primitive:

- Have you implemented the primitive at least twice, in two different surfaces?
- Did the two implementations converge on the same shape?
- Can you point at specific design pressures that shaped the convergence?

If the answer to all three is yes, the paper writes itself. If the answer to any is no, the paper is a hypothesis. Build more first.

---

Juan Cruz Maisú ♥
