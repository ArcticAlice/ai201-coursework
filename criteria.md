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
The city_guides documents are laid out clearly, with facts like bus frequencies 
and hospital locations stated right under headings such as “Getting there” and 
“Practical notes.” I set the bar at 4 of 5 because four of my questions point 
at obvious headings, but the “Where is parking free...” question shows up 
across several regional transport and accessibility guides, so the right 
chunk has more competition to beat.

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
Each document in city_guides has its own markdown file named after the 
town or topic (for example, guide_givens_mill.md). The grounding prompt 
tells the model to cite the filename of the chunk it used, and every 
retrieved chunk carries its file along with it. That makes 5 of 
5 realistic, as long as the model actually follows the prompt.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

**Why this target:**
The city_guides corpus is all about local UK towns, transport, and visitor logistics. 
Off-topic questions like engine maintenance, Rust syntax, or World Cup trivia score 
a cosine distance above 0.82, which is far past the 0.60 relevance cutoff. 

---

## 4. Something about your chunks

At least 4 of 5 sampled chunks read as a complete thought, with no sentence or 
heading cut in half at either boundary.


**Why this target:**
The city_guides corpus is organized with markdown headings (# Title and ## Section). 
A natve character window would chop sentences mid-word, like “station is a 15-”. 
Aiming for 4 of 5 checks that my custom chunker is splitting at section or paragraph 
boundaries instead of arbitrary character counts.

---

## 5. Your choice

For at least 4 of the 5 test questions, the top retrieved chunk originates from the 
primary guide dedicated to that specific town or cross-cutting topic rather than an 
unrelated town guide.


**Why this target:**
A lot of the town guides reuse the same subheadings, like “Practical notes” about 
mobile coverage. A well-behaved retriever should still rank the dedicated town 
guide first (guide_givens_mill.md for a Givens Mill question, say) over a more 
general regional guide, and I want that to hold for at least 4 of 5 queries.

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
