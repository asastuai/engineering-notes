# Fresh-context review

A second AI instance, running in a fresh conversation, reading the work cold, with explicit questions about where my reading missed something.

It is the highest-leverage move in the workflow that produced this stack.

---

## Why a second instance

When I work with an AI collaborator on a piece of writing, the collaboration is *with* the work. We are both inside the frame.

The AI helps sharpen claims, catches inconsistencies, pushes back on weak arguments, suggests citations. The collaboration is generative. It is good for what it is.

What it does not do is read the work the way someone outside the frame reads it.

The first reader of any artifact is not the author or the author's collaborator. The first reader is a stranger with no investment in defending the work's choices. Fresh-context review is a way to get that reader before the work goes public.

---

## The protocol

Three rules.

### A different instance, not the same one

The reviewer must be a fresh instance with no memory of the work-in-progress. Same model is fine. Same provider is fine. Different conversation history is non-negotiable.

The reason: an AI collaborator that has been inside the work for hours has internalized the author's framing. Asking it to review its own work produces a sympathetic review, not an adversarial one.

In practice: open a second tab, second window, second session. The second instance starts cold.

### Hand the work over with a brief, not a context dump

The reviewer needs three things to be useful:

- The artifact (paper draft, README, post, etc.).
- A one-paragraph context (who the author is, what the artifact is for, what state it is in).
- An explicit set of questions the reviewer should answer.

The questions are the load-bearing part. Without them, the reviewer drifts toward generic feedback. With them, the reviewer focuses on specific axes the author cannot see for themselves.

The questions used in this project:

1. Honesty check. Are there claims here that would not survive a careful look at the actual code?
2. Vocabulary consistency. Where does the technical vocabulary slip, lose precision, or get used loosely?
3. Voice integrity. Where does the writing slip back into AI-polish?
4. Strategic positioning. Will a serious reader take this seriously, or does it read as repackaged portfolio?
5. Holes. What would a hostile reviewer clip in five minutes?
6. Hardest-to-fix gap. The single thing that, if not fixed, will be the reason this does not work.

A seventh question gets added when the work is about to face hiring committees or funders:

7. Decision test. If you were the relevant decision-maker and this landed in your inbox cold, what do you do?

### Take the feedback as data, not as gospel

The reviewer is one cold reader. Their feedback is one signal. Some gets adopted. Some gets pushed back on with reasoning. Some gets noted for a future iteration.

The work that the reviewer's feedback earns is the *delta* between the author's blind spots and what the author would have shipped without the protocol.

---

## A specific exercise: pre-mortem questions

Before any high-stakes outreach, write down three questions that, if asked in a serious technical conversation, would cause you to go blank.

Not the questions already answered. The ones not yet.

For each, decide between:

- **(a) Prepare a real answer before outreach.** Worth the time if the question is likely to land in the first thirty minutes of a serious conversation.
- **(b) Pre-build a clean pivot.** *"I do not know yet. Here is how I would approach it: \[step\]. \[step\]. \[step\]."* Acceptable for questions outside the immediate frame of the work.

Option (b) is respectable in a research-lab conversation. Saying *I do not know yet* honestly is respected. Faking is not.

The exercise is uncomfortable. That is the point. The questions that produce going-blank are exactly the ones that need preparation.

I have run this exercise three times. Each time, two of three questions converted to (a). One stayed as (b). All three, prepared in advance, removed the situations in subsequent calls where I would have flailed.

---

## A note on the meta-loop

The reviewer is itself an AI. The reviewer can be wrong. The reviewer can hallucinate citations.

The protocol does not assume the reviewer is correct. The protocol assumes the reviewer is *cold*. The coldness is the value, not the correctness.

A cold reader who is sometimes wrong gives signal about which parts of the work are weakly grounded. Even when the reviewer's specific claim is wrong, the *fact that the reviewer reached for that claim* is information about how the work reads to a stranger.

Treat reviewer feedback like geophone readings. Some are noise. The pattern across them is signal.

---

## When to use the review

Three moments in the lifecycle of an artifact.

### Before publication

The most obvious. A draft that has been read adversarially before going public ships with fewer surface defects.

### Before high-stakes outreach

A paper or pitch about to be sent cold. The stakes are *being filtered out*; the author needs to know the filters in advance.

### After a rewrite

Whenever I rewrite a section in response to my own dissatisfaction, I pass the rewrite through the review. The reason: the rewrite was done to address something *I* saw. The reviewer reads it with no memory of what was being addressed. If the reviewer cannot tell what changed, the rewrite did not land.

---

## When not to use it

Most outputs are too small to deserve a review pass. The protocol is reserved for artifacts where shipping with a defect would cost meaningfully more than running the review.

A two-line README change does not get reviewed. A README rewrite does. A tweet does not. A blog post does.

The author decides per-artifact. The decision becomes faster with practice.

---

Juan Cruz Maisú ♥
