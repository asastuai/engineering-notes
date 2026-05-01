# The Inversion

The conventional research order is: paper first, code after.

The author writes a position paper. Reviewers respond. The paper is revised. Eventually a reference implementation is built, often by someone other than the author, often years later, often as evidence that the paper's claims hold up in practice.

i did the opposite.

i wrote the implementations first. The paper came after. The paper exists because the implementations needed grounding in something that argued for their shape, not the other way around.

This document explains the inversion, why it earned what it earned, and the boundaries of when it works.

---

## ◊ What the inversion looks like in practice

The Proof-of-Context family of papers exists because i first built five repositories that needed to talk to each other.

A pay-per-query data layer where every paid response had to be cryptographically pinned to the moment it was produced. A reputation registry where each agent's history had to be a function of verifiable commitments rather than vibes. A perpetual futures DEX where settlement had to gate against contextual freshness, not just signature validity. An agent wallet that had to refuse payment when the counterparty's data was stale. A Rust crate that had to encode the primitive everyone was reaching for.

Five repositories. One shared problem. No shared specification.

i built the implementations until the shape of the missing specification was undeniable. Then i wrote the paper that named what the implementations had been groping toward.

The paper did not invent the primitive. The paper named what was already there.

---

## What this earns

Three things.

### Empirical anchoring

The paper's claims are not abstract. Every claim in the v0.6 framework paper points at a real choice in a real implementation. The four freshness types are not philosophical decompositions of the staleness concept. They are the four things i found myself enforcing in different surfaces of the work, and which became indistinguishable at the boundary.

A reviewer who reads the paper can clone the repositories and verify that the claims hold up in production code. The chain of evidence is short.

### Adversarial pre-review

By the time the paper is being drafted, the implementations have already absorbed dozens of design pressures. The first version of the data layer's response shape was wrong. The second was partially wrong. The third worked. Each iteration removed an assumption the paper would otherwise have inherited.

The paper drafts inherit nothing. The implementations have already taken the hits.

### Convergence as evidence

Five independent surfaces (data, reputation, settlement, wallet, primitive crate) all reached for the same shape. That convergence is the central conceptual contribution of applied paper #2. The paper documents what the implementations had already produced.

A paper proposing the same shape *without* the implementations would be a hypothesis. With the implementations behind it, it is an observation.

---

## When this does not work

Two cases.

### When the primitive is genuinely novel

If you are inventing something the world has never seen, building five implementations of it before writing the paper is not feasible. You have to formalize before you can replicate. The inversion is for problems where the primitive is *findable* in the existing solution space — for cases where the paper's job is to name what is converging.

### When the implementations would be too expensive

Some primitives require months of engineering per implementation. Five of those is a multi-year commitment before any paper sees the light. The inversion works because each of the five repositories took weeks to a couple of months, not years.

If the primitive's natural implementation cost is high, the conventional paper-first order is correct. The implementations come later, by other people, and that is fine.

---

## ※ The honest version of why this happened

The inversion was not strategic. It was the only thing i could do.

i had no academic affiliation. No co-authors. No reviewer pool to address. The standard incentives that produce paper-first order were not present in my situation.

What i had was time, AI collaboration, and a willingness to ship public repositories before any paper existed. That setup made the inversion possible. A traditional research career setup would have made it impossible.

This is worth saying because the inversion is not a discovery. It is what an independent researcher does when the conventional gates are not in the way.

If you are an independent researcher reading this, the conventional gates are not in your way either.

---

## ❖ How to apply the inversion

If you are about to write a paper proposing a new primitive, ask yourself:

- Have you implemented the primitive at least twice, in two different surfaces?
- Did the two implementations converge on the same shape?
- Can you point at specific design pressures that shaped the convergence?

If the answer to all three is yes, the paper writes itself. The inversion has done its work.

If the answer to any is no, the paper is a hypothesis. The inversion is not yet earned. Build more before formalizing.

---

Juan Cruz Maisú ♥
