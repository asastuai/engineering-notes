# The Adversarial Review

A second AI instance, running in a fresh context, reading my work cold, looking for the places where my own reading missed something.

That is the protocol. It is small. It is the highest-leverage move in the working method.

---

## ◊ Why this exists

When i work with an AI collaborator on a piece of writing, the collaboration is *with* the work. We are both inside the frame.

The AI helps me sharpen claims. It catches inconsistencies. It pushes back on weak arguments. It suggests citations. The collaboration is generative. It is good for what it is.

What it does not do is read the work the way someone outside the frame reads it.

The first reader of any artifact is not the author or the author's collaborator. The first reader is a stranger who has not absorbed any of the context the author and the collaborator built up. That stranger sees the work with no investment in defending its choices.

Adversarial review is the protocol for getting that reader before the work goes public.

---

## How the protocol works

Three rules.

### Rule 1: a different instance, not the same one

The reviewer must be a fresh instance with no memory of the work-in-progress. Same model is fine. Same provider is fine. Different conversation history is non-negotiable.

The reason: an AI collaborator that has been inside the work for hours has internalized the author's framing. Asking it to review its own work produces a sympathetic review, not an adversarial one.

In practice, the author opens a second tab. Or a second window. Or a second session in the same client. The second instance starts cold.

### Rule 2: hand the work over with a brief, not a context dump

The reviewer needs three things to be useful:

- The artifact (paper draft, README, post, whatever).
- A one-paragraph context (who the author is, what the artifact is for, what state it is in).
- An explicit set of questions the reviewer should answer.

The questions are the load-bearing part. Without them, the reviewer drifts toward generic feedback ("this is well-written but could be more concise"). With them, the reviewer focuses on specific axes the author cannot see for themselves.

The questions i use:

1. Honesty check. Are there claims here that would not survive a careful look at the actual code or repository?
2. Vocabulary consistency. Where does the technical vocabulary slip, lose precision, or get used loosely?
3. Voice integrity. Where does the writing slip back into AI-polish?
4. Strategic positioning. Will a serious reader take this seriously, or does it read as repackaged portfolio?
5. Holes. What would a hostile reviewer clip in five minutes?
6. Hardest-to-fix gap. The single thing that, if not fixed, will be the reason this does not work.

A seventh question gets added when the work is about to face hiring committees or funders:

7. Decision test. If you were a hiring lead at \[target organization\] and this landed in your inbox cold, what do you do? Email back asking what specifically? Archive for later? Ignore?

### Rule 3: take the feedback as data, not as gospel

The reviewer is one cold reader. Their feedback is one signal. It is the most valuable signal the author has access to before publication, but it is not the truth.

The author reads the feedback. The author decides. Some of the feedback gets adopted. Some gets pushed back on with reasoning. Some gets noted for a future iteration.

The work that the reviewer's feedback earns is the *delta* between the author's blind spots and the public version of the artifact. That delta is what the author would have shipped without the protocol versus what the author ships with it.

---

## ❖ The Q-terror exercise

A specific protocol that i use before any high-stakes outreach.

The author writes down three questions that, if asked in a serious technical conversation, would make them go blank.

Not the questions the author has answered already. The ones the author has not.

For each of the three, decide between:

- **(a) Prepare a real answer before outreach.** Worth the time if the question is likely to land in the first thirty minutes of any serious conversation.
- **(b) Pre-build a clean pivot.** *"i do not know yet. Here is how i would approach it. One: \[step\]. Two: \[step\]. Three: \[step\]."* Acceptable for questions outside the immediate frame of the work.

Option (b) is respectable in a research-lab conversation. Saying *i do not know yet* honestly is respected. Faking is not.

The exercise is uncomfortable. That is the point. The questions that make the author go blank are exactly the ones that need preparation.

i have run the Q-terror exercise three times so far. Each time, two of the three questions converted to (a) (prepared answer). One stayed as (b) (clean pivot). All three, prepared in advance, removed the only situations in subsequent calls where i would have flailed.

---

## ※ A note on the meta-loop

The reviewer instance is itself an AI. The reviewer can be wrong. The reviewer can be sycophantic. The reviewer can hallucinate citations.

The protocol does not assume the reviewer is correct. The protocol assumes the reviewer is *cold*. The coldness is the value, not the correctness.

A cold reader who is sometimes wrong gives the author signal about which parts of the work are weakly grounded. Even when the reviewer's specific claim is wrong, the *fact that the reviewer reached for that claim* is information about how the work reads to a stranger.

The author treats reviewer feedback like geophone readings during exploration. Some of the readings are noise. The pattern across the readings is the signal.

---

## ◊ When the adversarial review does most work

Three moments in the lifecycle of an artifact.

### Before publication

The most obvious. A draft that has been read adversarially before going public ships with fewer surface defects than one that has not.

### Before high-stakes outreach

A paper or a pitch that is about to be sent cold to a research lab, a VC, a grant committee. The stakes are *being filtered out*, which means the author needs to know the filters in advance.

### After a rewrite

Whenever i rewrite a section in response to my own dissatisfaction, i pass the rewrite through adversarial review. The reason: the rewrite was done to address something *i* saw. The reviewer reads it with no memory of what was being addressed. If the reviewer cannot tell what changed, the rewrite did not land.

---

## How the protocol scales

It scales because the cost is low.

A second AI instance is free if the author has access to one. Twenty minutes of the reviewer's time produces feedback that takes the author hours to act on. The asymmetry is in the author's favor.

It does not scale to *every* output. Most outputs are too small to deserve a review pass. The protocol is reserved for artifacts where shipping with a defect would cost the author meaningfully more than running the review.

A two-line README change does not get reviewed. A README rewrite does. A tweet does not. A blog post does.

The author decides per-artifact. The decision becomes faster with practice.

---

Juan Cruz Maisú ♥
