# The Unofficial Guide

Jawad Bhullar & Corpus: city_guides

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

I picked the corpus city_guides. This corpus purpose is to answer questions 
related to vacation spots in certain areas. These questions are based on reviews
and other comments left by people who have vistied the area. The system answers 
questions such as "What are reccomendations on places to eat?", "What form of 
transportation is available to reach [destination]?".  

## Chunking Strategy

**Chunk size:** Chunk sizes differ because it based on section titles instead.
**Overlap:** There isn't much overlap since the cut offs are by sections.

When I looked through the documents in `corpora/city_guides/`, I saw that all 14 documents are structured Markdown files with clear `# Town Name` titles and `## Section` headings. Instead of arbitrary character counts, my chunker splits documents along `## ` markdown section boundaries while preserving the document title as header context. This ensures every chunk reads as a complete, standalone thought.

## Sample Chunks

======================================================================
Chunk 1  |  source: thread_bike_commute.txt#0  |  produced by: chunker.py::fallback_split
======================================================================
THREAD: Is a bike worth it for a 20 minute walk commute?

--- reply 1 (14 votes) ---
Yeah. Cuts an 18 minute walk to about 6. The thing nobody mentions is storage — covered bike parking exists at three buildings and is full by 9am at all three.

--- reply 2 (9 votes) ---
Counterpoint, I sold mine. Between November and March the paths are either icy or salted and salt destroys a drivetrain in one season.

--- reply 3 (22 votes) ---
Both true. I keep a cheap bike for September to November and walk the rest of the year. Total cost was about $120 for the bike and I don't care what happens to it.

--- reply 4 (5 votes) ---
If you do get one, the campus does free registration and it's the only reason I got mine back after it was taken.

**Chunk 1** — source: `` — produced by: ``

======================================================================
Chunk 1  |  source: guide_accessibility.md#0  |  produced by: chunker.py::split_documents
======================================================================
# Getting around the region with limited mobility

An honest assessment rather than a promotional one. Some of these places are
difficult and it is better to know in advance.

**Chunk 2** — source: `` — produced by: ``

======================================================================
Chunk 2  |  source: guide_corry_vale.md#6  |  produced by: chunker.py::split_documents
======================================================================
# Corry Vale

## When to go
May to September. Outside those months the pub in the third village closes, the farm shop reduces its hours, and several footpaths become genuinely boggy rather than merely wet. The road is not gritted above the second village and is impassable in snow.

**Chunk 3** — source: `` — produced by: ``

======================================================================
Chunk 3  |  source: guide_givens_mill.md#3  |  produced by: chunker.py::split_documents
======================================================================
# Givens Mill

## Eat and drink
A tearoom attached to the mill, open 10 to 4 daily except Tuesdays, which sells bread made from the flour ground twenty metres away and is the reason most people come. One pub, food served lunchtimes and Thursday to Saturday evenings.

**Chunk 4** — source: `` — produced by: ``

======================================================================
Chunk 4  |  source: guide_kestrelford.md#6  |  produced by: chunker.py::split_documents
======================================================================
# Kestrelford

## When to go
Late spring and early autumn. The Saturday market runs year-round but is much reduced from November to February. August is busy with walkers. The single-track approach road is genuinely difficult in snow and the town can be cut off for a day or two most winters.

**Chunk 5** — source: `` — produced by: ``

======================================================================
Chunk 5  |  source: guide_regional_transport.md#1  |  produced by: chunker.py::split_documents
======================================================================
# Getting around the region

## The railway
The line runs along the river valley, connecting Brightwater to the regional
hub in 50 minutes. Eleven services a day on weekdays, six on Sundays. The line
north of Brightwater closed in 1963 and everything beyond it is bus or car.

Tickets are cheaper booked the day before than on the day, and considerably
cheaper than that booked a week ahead. There is no ticket office at
Brightwater station outside weekday mornings; the machine on the platform takes
cards only.

## Sample Answer

**Question:** 

How many buses a day run from Brightwater to Givens Mill on weekdays?

**Answer:**

Four buses a day run from Brightwater to Givens Mill on weekdays. 

Source: guide_givens_mill.md

Sources retrieved: guide_brightwater.md, guide_givens_mill.md, guide_kestrelford.md, guide_regional_transport.md

**My relevance cutoff:**

I left the number at 0.6 as the thresehold because based on the results I
got from the questions I asked they seemed to fit in the range. On one of
the questions I asked that was supposed to be in corpus I get a best distance
of 0.502 which is towards the higher end. If I made the thresehold smaller
a question like that would not be answered. On average the gap was around
a .5 difference between questions that were in corpus and those that weren't.

| Question                                                              | In corpus? | Best distance |
| --------------------------------------------------------------------- | ---------- | ------------- |
| How many buses a day run from Brightwater to Givens Mill on weekdays? | Yes        | 0.317         |
| "Where is parking free for two hours anywhere in town?"               | Yes        | 0.502         |
| "Which months are recommended to visit Corry Vale?"                   | Yes        | 0.353         |
| "How often does the Marchwood tram network run on weekdays?"          | Yes        | 0.202         |
| "Where is the nearest full hospital to Halden Bay?"                   | Yes        | 0.336         |
| "What is the capital of Mongolia?"                                    | No         | 0.754         |
| "How do I change the oil in a diesel engine?"                         | No         | 0.888         |
| "Who won the 1994 World Cup?"                                         | No         | 0.899         |
| "What is the recommended dosage of ibuprofen for a headache?"         | No         | 0.835         |
| "How do I write a for loop in Rust?"                                  | No         | 0.836         |

## How I Used AI

**1.**

Once I looked through corpora files for city guides I saw that most of 
documents were seperated by headers. I used that information and prompted 
chatgpt to write the code for the chunking function that would serparte it 
based on the headers. The function worked well so I didn't have to change 
anything.

**2.**

Another moment I asked AI was to help me create a question that
would produce a best distance close to the thresehold. Originally the 
questions I came up with were either well within the thresehold or too 
far away. I asked chatgpt and it gave me the question "Where is parking 
free for two hours anywhere in town?". I used that and it gave me a best 
distance value of .5 which was close to what I was looking for. 

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion                              | Target | Run 1 | Run 2 | Run 3 | Verdict |
| -------------------------------------- | ------ | ----- | ----- | ----- | ------- |
| 1. Retrieved chunk contains the answer | 4 of 5 |       |       |       |         |
| 2. Every answer names a source         | 5 of 5 |       |       |       |         |
| 3. Gate stops out-of-corpus questions  | 4 of 5 |       |       |       |         |
| 4.                                     |        |       |       |       |         |
| 5.                                     |        |       |       |       |         |

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| #   | Criterion | Verdict | How I decided |
| --- | --------- | ------- | ------------- |
| 1   |           |         |               |
| 2   |           |         |               |
| 3   |           |         |               |
| 4   |           |         |               |
| 5   |           |         |               |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion                              | Target | Run 1 | Run 2 | Run 3 | Verdict |
| -------------------------------------- | ------ | ----- | ----- | ----- | ------- |
| 1. Retrieved chunk contains the answer | 4 of 5 |       |       |       |         |
| 2. Every answer names a source         | 5 of 5 |       |       |       |         |
| 3. Gate stops out-of-corpus questions  | 4 of 5 |       |       |       |         |
| 4.                                     |        |       |       |       |         |
| 5.                                     |        |       |       |       |         |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
