# The Hardening Pipeline

Eight phases. Applied to four repositories that had been "casi oneshoteadas" (almost-oneshotted). Took them from no-tests-and-aspirational-claims to forty-three integration tests passing, signed Ed25519 attestations on every paid endpoint, and an honest README per repo.

The pipeline is what i run when a freshly-written repository needs to become outreach-defensible.

---

## ◊ What "casi oneshoteado" means

A repository written in one or two intense AI-assisted sessions, where:

- The code compiles and runs.
- Some endpoints work.
- The README claims more than the code delivers.
- There are no tests, or there are tests that test the AI's first guess of the API rather than the actual behavior.
- Vulnerabilities exist in transitive dependencies.
- The threat model is assumed but not stated.
- The integration with sibling repositories is described but not implemented.

This is not a moral failing. It is what shipping fast with AI tools produces. The repos hit a useful milestone (something runnable in days instead of months). The hardening pipeline is what closes the gap between *runnable* and *outreach-defensible*.

---

## The eight phases

Each phase has a clear input, a clear output, and a clear gate. Phases run sequentially per repo. Multiple repos can run their phases in parallel.

### Phase 1: reconnaissance audit

Clone the repo. Inventory files, languages, build system, test framework. Run the build. Run the tests (or note their absence). Boot the service if applicable. Hit the documented endpoints.

Output: an audit document at `audits/audit-<repo>.md` that catalogs what runs, what does not, and what the README claims that the code does not deliver.

Gate: every claim in the README is either verified, falsified, or marked as roadmap.

### Phase 2: adversarial pass

Walk the code looking for security smells, missing input validation, race conditions, resource exhaustion paths. Identify rate-limiting gaps, CORS too-permissive, missing schema validation, vulnerable dependencies. Compose a threat model honest about which adversaries are in scope and which are not.

Output: an attack document or an extended audit document with vulnerabilities listed in priority order.

Gate: critical and high-severity vulnerabilities have remediation plans (even if the implementation lands in Phase 4).

### Phase 3: PoC integration design

Identify where the project's primary primitive (in this case, Proof-of-Context) integrates. For each integration point: which freshness type applies, what the commitment shape is, what verification looks like, what the gas / latency cost is.

Output: an integration design document at `audits/poc-integration-<repo>.md` with specific function signatures and integration cost estimates.

Gate: a senior engineer reading the design could implement Phase 4 from it without further context.

### Phase 4: refuerzo execution

Implement the integration. Add tests. Fix the high-priority vulnerabilities from Phase 2. Build a working demo flow end-to-end. Update package versions, fix npm audit findings, update transitive deps where possible.

Output: code changes, test additions, dependency updates. Commit with a message that ties to the audit document.

Gate: tests pass. Demo flow works. README still aligned with new code state.

### Phase 5: verification + sync

Re-run the test suite. Re-deploy if the project has a deployment surface. Update the README to reflect the actual state. Verify cross-links between sibling repositories and the umbrella documentation.

Output: README sync, version bump, tag.

Gate: README is honest about every claim. Status table reflects current reality. No claim is overstated.

### Phase 6: distribution preparation

Outline papers, drafts of blog posts, demo video scripts, social media announcement copy. Anything that turns the work into things readers can encounter.

Output: paper outlines and abstracts, post drafts, video scripts, announcement copy.

Gate: an outsider, given only the distribution materials, could understand the work without reading the code.

### Phase 7: cosmetic sweep

Apply the voice canon (signature, glyph alphabet) to every README. Remove decorative emojis. Add deliberate glyphs where they earn their position. Verify cross-linking is complete and consistent across repositories.

Output: small cosmetic commits per repo, individually pushed.

Gate: every repo's README looks like it was authored by the same hand without losing per-repo identity.

### Phase 8: report for adversarial review

Compile a comprehensive report covering everything that happened in phases 1-7. Hand the report to a fresh AI instance for adversarial review. Process the feedback. Apply the high-leverage fixes. Re-publish.

Output: a formal report at `REPORT-FOR-CLASSIC-<date>.md`. A revised set of artifacts after the review.

Gate: at least one round of adversarial review has been processed. The author can articulate what changed in response.

---

## ❖ Why eight phases and not fewer

Earlier versions of this pipeline had four phases. Then five. Then seven. The current version stabilized at eight after running it through four real repositories.

The phases that resisted being collapsed:

- Phase 2 cannot be merged into Phase 1. The audit is descriptive. The adversarial pass is *adversarial*. They use different mental modes.
- Phase 3 cannot be merged into Phase 4. Designing the integration before building it forces the design to be defensible on its own. Building first and documenting after produces patches that look like designs.
- Phase 7 cannot be merged into Phase 5. The cosmetic sweep is its own register. Mixing it into the README sync invites scope creep.
- Phase 8 cannot be skipped. Every previous round of adversarial review caught at least one defect that the author had not seen.

Eight phases is the floor. Some specific repositories want a ninth (security audit by a third party, mainnet deployment plan, etc.). Eight is what a typical repo deserves.

---

## How long the pipeline takes

For a repository in the state described at the top of this document, a single experienced practitioner running the pipeline with AI assistance takes:

- Phase 1: 30 to 60 minutes.
- Phase 2: 30 to 90 minutes.
- Phase 3: 30 to 60 minutes.
- Phase 4: 1 to 4 hours, depending on the complexity of the integration.
- Phase 5: 30 to 60 minutes.
- Phase 6: 1 to 3 hours, depending on whether papers and videos are full drafts or outlines.
- Phase 7: 15 to 30 minutes per repo.
- Phase 8: 1 to 2 hours plus the time to process the review.

A four-repo run, executed in series, lands at 25 to 35 hours of focused work. Executed with two repos in parallel where possible, 18 to 24 hours.

This is realistic. The author has done it twice.

---

## ※ When the pipeline does not apply

Two cases.

### When the repo is too small to deserve it

A 200-line script with three users does not need eight phases of hardening. The investment outpaces the return. The pipeline applies to repositories with public claims, integration surfaces, or production stakes.

### When the repo is being abandoned

If the author has decided the repository is no longer load-bearing for the work going forward, the pipeline is wasted. Archive the repo. Document why it was archived. Move on.

The pipeline is for repositories that are *staying*.

---

## ◊ A diagnostic before starting

Before running the pipeline on a repo, ask:

- Does this repo have a README that claims things the code may not deliver?
- Are there integration claims with sibling repositories that have not been implemented?
- Are there vulnerable dependencies that have not been remediated?
- Is the threat model implicit or absent?

If the answer to two or more is yes, the pipeline is appropriate. If the answer to all four is no, the repo is already in good shape and only needs Phase 7 (cosmetic) and Phase 8 (review).

The diagnostic is what tells the author where to start, not whether to start. Every public-facing repo passes through Phase 7 and Phase 8 at minimum.

---

Juan Cruz Maisú ♥
