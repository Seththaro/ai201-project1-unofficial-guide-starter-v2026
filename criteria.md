# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
<!-- e.g. "One of my questions is about a topic only two documents mention, so
     I expect that one to be hard." -->

I picked 4 of 5 because at least one of my questions is covered by only one or
two posts, so I expect that one to be hard to retrieve. I didn't pick 5 of 5 because
one miss shouldn't fail the whole system, and I didn't pick 3 of 5 because that would
let a weak retriever pass.

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
<!-- Why all five and not four? What about your setup makes that achievable —
     or what would have to go wrong for it not to be? -->

I picked all five because the starter's grounding instruction already tells the model
to name the source file, so a missing source would mean my prompt or code broke, not
that the task is hard. It would only fail if the model ignores the instruction or a
chunk reaches it without a filename.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:**
<!-- What did your distances look like when you set the cutoff in Milestone 4?
     Was there a clean gap, or did the two groups overlap? -->

I picked 4 of 5 because an out-of-scope question can share a few words with my
corpus and land close to the cutoff. My in-corpus questions had best distances
of ___ to ___, and the out-of-scope questions had ___ to ___. [Say whether there
was a clean gap or the groups overlapped.] I set my cutoff at ___ because ___.

---

## 4. Something about your chunks

<!-- YOU WRITE THIS ONE.

     How would you know if your chunks were the right size? Name something
     countable or observable.

     Examples of the right shape — don't copy these, they should come from
     what you actually saw in Milestone 3:
       - "At least 4 of 5 sampled chunks read as a complete thought, with no
          sentence cut in half at either end."
       - "No chunk is shorter than 200 characters, since anything below that
          in my corpus turned out to be a heading with no content under it." -->

For at least 4 of my 5 test questions, the top retrieved chunk answers the
question on its own, without needing the chunk before or after it. I check
this by reading each top chunk and asking whether someone could answer the
question from that text alone.

**Why this target:**

I picked 4 of 5 because one question may depend on details spread
across two posts, and I don't want one odd case to fail the whole system.
I did not pick 5 of 5 because a single chunk that is split slightly wrong
would then count as a total failure. I did not pick 3 of 5 because that
would let a chunker that cuts thoughts in half pass.

---

## 5. Your choice

<!-- YOU WRITE THIS ONE TOO.

     Pick something you actually care about getting right. It could be about
     speed, about refusals, about a particular kind of question your corpus
     handles badly, about source attribution being correct rather than merely
     present — anything, as long as it names a number or an observable
     outcome. -->

Every answer is 120 words or fewer, and every fact in it appears in the
retrieved chunks. I check the length with a word count and the facts by
comparing each claim to the chunk text.

**Why this target:**

I chose this because the main risk in this project is a confident
answer that sounds right but came from the model's own knowledge. Keeping
answers short leaves less room for extra claims, and a 120 word limit is
long enough to give a useful answer with a source. I picked a strict rule
of "every answer" instead of "most answers" because one made-up fact is
enough to make a guide untrustworthy.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
