# Hardening pipeline

Eight phases applied to four repositories that started in an under-tested, under-documented state and ended outreach-defensible. This note documents the phases, what each one produces, and where the pipeline applies or does not.

---

## The starting state

In this project, four agent-economy repositories were initially built in one or two intense AI-assisted sessions each. After those initial pushes:

- The code compiled and ran.
- Some endpoints worked.
- The README claimed more than the code delivered.
- There were no tests, or there were tests that tested the AI's first guess of the API rather than the actual behavior.
- Vulnerabilities existed in transitive dependencies.
- The threat model was assumed but not stated.
- Integration with sibling repositories was described but not implemented.

This is not a moral failing. It is what shipping fast with AI tools tends to produce. The repos hit a useful milestone (something runnable in days instead of months). The hardening pipeline is what closes the gap between *runnable* and *outreach-defensible*.

---

## The eight phases

Each phase has a clear input, a clear output, and a clear gate. Phases run sequentially per repo. Multiple repos can run their phases in parallel.

### Phase 1: reconnaissance audit

Clone the repo. Inventory files, languages, build system, test framework. Run the build. Run the tests. Boot the service if applicable. Hit the documented endpoints.

Output: an audit document that catalogs what runs, what does not, and what the README claims that the code does not deliver.

Gate: every claim in the README is either verified, falsified, or marked as roadmap.

### Phase 2: adversarial pass

Walk the code looking for security smells, missing input validation, race conditions, resource exhaustion paths. Identify rate-limiting gaps, CORS too-permissive, missing schema validation, vulnerable dependencies. Compose a threat model honest about which adversaries are in scope and which are not.

Output: an attack document or extended audit document with vulnerabilities listed in priority order.

Gate: critical and high-severity vulnerabilities have remediation plans (even if the implementation lands in Phase 4).

### Phase 3: integration design

Identify where the project's primary primitive integrates. For each integration point: which type or layer applies, what the data shape is, what verification looks like, what the cost is.

Output: an integration design document with specific function signatures and integration cost estimates.

Gate: another engineer reading the design could implement Phase 4 from it without further context.

### Phase 4: implementation

Implement the integration. Add tests. Fix the high-priority vulnerabilities from Phase 2. Build a working flow end-to-end. Update package versions, fix audit findings, update transitive deps where possible.

Output: code changes, test additions, dependency updates. Commit with a message that ties to the audit document.

Gate: tests pass. Flow works. README still aligned with new code state.

### Phase 5: verification + sync

Re-run the test suite. Re-deploy if applicable. Update the README to reflect the actual state. Verify cross-links between sibling repositories and umbrella documentation.

Output: README sync, version bump, tag.

Gate: README is honest about every claim. Status table reflects current reality. No claim is overstated.

### Phase 6: distribution preparation

Outline papers, drafts of blog posts, demo video scripts, social media announcement copy. Anything that turns the work into things readers can encounter.

Output: paper outlines and abstracts, post drafts, video scripts, announcement copy.

Gate: an outsider, given only the distribution materials, could understand the work without reading the code.

### Phase 7: cosmetic sweep

Apply consistent styling and signatures to every README. Verify cross-linking is complete and consistent across repositories.

Output: small cosmetic commits per repo, individually pushed.

Gate: every repo's README looks like it was authored by the same hand without losing per-repo identity.

### Phase 8: report for review

Compile a comprehensive report covering everything in phases 1-7. Hand the report to a fresh reviewer (see `02-fresh-context-review.md`). Process the feedback. Apply the high-leverage fixes. Re-publish.

Output: a formal report. A revised set of artifacts after the review.

Gate: at least one round of fresh-context review has been processed. The author can articulate what changed in response.

---

## Why eight and not fewer

Earlier versions had four phases. Then five. Then seven. The current version stabilized at eight after running it through four real repositories.

The phases that resisted being collapsed:

- Phase 2 cannot be merged into Phase 1. The audit is descriptive. The adversarial pass is *adversarial*. They use different mental modes.
- Phase 3 cannot be merged into Phase 4. Designing the integration before building it forces the design to be defensible on its own.
- Phase 7 cannot be merged into Phase 5. The cosmetic sweep is its own register. Mixing it into the README sync invites scope creep.
- Phase 8 cannot be skipped. Every previous round of fresh-context review caught at least one defect that the author had not seen.

Eight phases is the floor for the kind of project this was. Some repositories want a ninth (security audit by a third party, mainnet deployment plan, etc.).

---

## How long it takes

For a repository in the starting state described above, an experienced practitioner running the pipeline with AI assistance takes:

- Phase 1: 30 to 60 minutes.
- Phase 2: 30 to 90 minutes.
- Phase 3: 30 to 60 minutes.
- Phase 4: 1 to 4 hours, depending on the complexity of the integration.
- Phase 5: 30 to 60 minutes.
- Phase 6: 1 to 3 hours, depending on whether papers and videos are full drafts or outlines.
- Phase 7: 15 to 30 minutes per repo.
- Phase 8: 1 to 2 hours plus the time to process the review.

A four-repo run in series lands at 25 to 35 hours of focused work. With two repos in parallel where possible, 18 to 24 hours.

---

## When the pipeline does not apply

### Repos too small to deserve it

A 200-line script with three users does not need eight phases. The investment outpaces the return. The pipeline applies to repositories with public claims, integration surfaces, or production stakes.

### Repos being abandoned

If the repository is no longer load-bearing for the work going forward, the pipeline is wasted. Archive the repo. Document why. Move on.

The pipeline is for repositories that are *staying*.

---

## A diagnostic before starting

Before running the pipeline on a repo:

- Does this repo have a README that claims things the code may not deliver?
- Are there integration claims with sibling repositories that have not been implemented?
- Are there vulnerable dependencies that have not been remediated?
- Is the threat model implicit or absent?

If two or more answers are yes, the pipeline is appropriate. If all four are no, only Phase 7 (cosmetic) and Phase 8 (review) are needed. Every public-facing repo passes through at least Phase 7 and Phase 8 at minimum.

---

Juan Cruz Maisú ♥
