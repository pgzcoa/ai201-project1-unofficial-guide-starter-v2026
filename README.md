# The Unofficial Guide

<!-- Patricia Guerrero
Replace this line  and which corpus you picked. -->

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

<!-- Three or four sentences. Which corpus you picked, and the kinds of
     questions your system answers. Write it for someone who has never seen
     this repo.

     This project is a retrieval-augmented question-answering system built using the campus_life corpus.  It retrieves information from campus-life documents and uses the most relevant documents to answer questions about topics such as academics, housing, dining, parking, and graduation requirements.  The system only answers questions when the retrieved information is relevant enough and uses the retrieved documents as the source for its answers. Questions outside the information covered by the corpus are rejected instead of being answered with guesses.

     Milestone 5. -->

## Chunking Strategy

**Chunk size:** 1 complete post
**Overlap:** 0

I kept each campus-life post as one chunk because the posts are already short and usually contain a complete piece of information.  This avoids splitting a useful answer across multiple chunks.  The resulting chunks have an average length of about 317 characters, with the shortest at 178 characters, and the longest and 549 characters.  I used 0 to overlap because each post is kept intact and does not need information repeated from another chunk.

## Sample Chunks

 <!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     ======================================================================
Chunk 1  |  source: admin_add_drop_deadline.txt#0  |  produced by: chunker.py::split_documents
======================================================================
On the add/drop deadline

You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.

======================================================================
Chunk 2  |  source: course_biol_160.txt#0  |  produced by: chunker.py::split_documents
======================================================================
BIOL 160 Cell Biology

I lived here my sophomore year. Format is lecture three times a week with a weekly lab. Assessment: four unit tests and a cumulative final. Not curved.

Expect 9 to 11 hours a week, the heaviest first-year course by reputation.

The one piece of advice: the unit tests come fast, roughly every three weeks; falling behind once is very hard to recover from.

======================================================================
Chunk 3  |  source: course_hist_118_workload.txt#0  |  produced by: chunker.py::split_documents
======================================================================
Workload for HIST 118 Modern World History

People keep asking so: a lot of reading, about 120 pages a week, but no problem sets. That's real time, not optimistic time.

It's front-loaded — the first month is heavier than the rest, partly because you're learning the format.

======================================================================
Chunk 4  |  source: dining_pellew_dining_hall_followup.txt#0  |  produced by: chunker.py::split_documents
======================================================================
Re: Pellew Dining Hall

Adding to what people have said about Pellew Dining Hall. The wait figure of 12 to 18 minutes at peak matches what I've seen. If you're trying to eat between classes, go before 11:45 and it's a different building entirely.

Also worth saying: the furthest hall from anywhere, next to the athletics centre. Nobody tells you this at orientation.

======================================================================
Chunk 5  |  source: housing_innisfree_hall.txt#0  |  produced by: chunker.py::split_documents
======================================================================
Innisfree Hall — what it's actually like

Transferred in last year, so take this with a grain of salt. Built 1991, renovated 2022. Rooms are doubles arranged as pairs sharing one bathroom between two rooms.

The good: the shared-bathroom-between-two-rooms arrangement is the best compromise on campus.

The bad: no air conditioning, which matters for the first three weeks of September.

Laundry costs $1.75 wash, $1.75 dry, app-based. On noise: moderate; the building is L-shaped and the short wing is much quieter.

     Milestone 3. -->

**Chunk 1** — source: admin_add_drop_deadline.txt0 `` — produced by: ``chunker.py::split_documents

```On the add/drop deadline
```You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.

**Chunk 2** — source: ``course_biol_160.txt#0 — produced by: chunker.py::split_documents ``

```BIOL 160 Cell Biology 
```I lived here my sophomore year. Format is lecture three times a week with a weekly lab. Assessment: four unit tests and a cumulative final. Not curved. Expect 9 to 11 hours a week, the heaviest first-year course by reputation. The one piece of advice: the unit tests come fast, roughly every three weeks; falling behind once is very hard to recover from.

**Chunk 3** — source: `course_hist_118_workload.txt#0` — produced by: `chunker.py::split_documents`

```Workload for HIST 118 Modern World History
```Adding to what people have said about Pellew Dining Hall. The wait figure of 12 to 18 minutes at peak matches what I've seen. If you're trying to eat between classes, go before 11:45 and it's a different building entirely. Also worth saying: the furthest hall from anywhere, next to the athletics centre. Nobody tells you this at orientation.

**Chunk 4** — source: `dining_pellew_dining_hall_followup.txt#0` — produced by: `chunker.py::split_documents`

```Re: Pellew Dining Hall
```Adding to what people have said about Pellew Dining Hall. The wait figure of 12 to 18 minutes at peak matches what I've seen. If you're trying to eat between classes, go before 11:45 and it's a different building entirely. Also worth saying: the furthest hall from anywhere, next to the athletics centre. Nobody tells you this at orientation.

**Chunk 5** — source: `housing_innisfree_hall.txt#0` — produced by: `chunker.py::split_documents`

```Innisfree Hall - what it's actually like
```Transferred in last year, so take this with a grain of salt. Built 1991, renovated 2022. Rooms are doubles arranged as pairs sharing one bathroom between two rooms. The good: the shared-bathroom-between-two-rooms arrangement is the best compromise on campus. The bad: no air conditioning, which matters for the first three weeks of September. Laundry costs $1.75 wash, $1.75 dry, app-based. On noise: moderate; the building is L-shaped and the short wing is much quieter.

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:**

**Answer:**

```**Question:** When do students declare a major?

**Answer:** Students declare at the end of their second semester, or later if needed.

**Source:** `admin_declaring_a_major.txt`

```

**My relevance cutoff:**

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     I kept the cutoff at 0.6 because there was a clear gap between the questions my corpus covers and the questions that are out of scope.  The five covered questions had best distances from 0.221 to 0.380.  The five out-of-scope questions had best distances from 0.825 to 0.934.  The 0.6 cutoff falls between these two groups, so it separates the relevant questions from the unrelated questions. 

     Milestone 4. -->

| Question | In corpus? | Best distance |
|---|---|---|
|How long does an interlibrary loan request usually take?  | yes  | 0.380  |
|When do students declare a major?                         | yes  | 0.372  |
|How quickly do west-lot parking permits usually sell out? | yes  | 0.221  |
|How many credit hours are required for graduation?        | yes  | 0.268  |
|What is the best time to do laundry in Morrow House?	    | yes  | 0.305  |
|What is the capital of Mongolia?	                        |  no	 | 0.825  |
|How do I change the oil in a diesel engine?               |  no  | 0.934  |
|Who won the 1994 World Cup?	                             |  no	 | 0.886  |
|What is the recommended dosage of ibuprofen for a headache?| no	 | 0.844  |
|How do I write a for loop in Rust?                        |  no  | 0.896  |


## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.**to help troubleshoot dependency issues while setting up my project. When I encountered errors installing packages, I shared the error messages and got suggestions for resolving missing dependencies and Python version conflicts. I had conflicts going between 2 different python versions because one was not compatible.

**2.**I followed the troubleshooting steps, checked that the packages were installed in my project's virtual environment, and verified that ChromaDB was working.


<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->
**Stretch Feature: Metadata filtering**

I am adding metadata filtering so retrieval can be narrowed by document source. I will compare the same query with and without a source filter and document how the retrieved results change.

I tested the same question with and without a source filter.

**Question:** When do students declare a major?

**Without filter:**
- `admin_declaring_a_major.txt` — distance 0.372
- `admin_pass_fail_option.txt` — distance 0.509
- `admin_graduation_requirements.txt` — distance 0.589
- `admin_add_drop_deadline.txt` — distance 0.638
- `admin_study_abroad.txt` — distance 0.682

**With source filter:** `admin_declaring_a_major.txt`
- `admin_declaring_a_major.txt` — distance 0.372

**What changed:** Without the filter, retrieval returned five results from different documents. With the source filter, retrieval was narrowed to the specified document, so only `admin_declaring_a_major.txt` was returned. The relevant result and its distance stayed the same because it was already the closest match.
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

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5 of 5 |5 of 5  | 5 of 5 | MET |
| 2. Every answer names a source | 5 of 5 | 5 of 5 | 5 of 5  | 5 of 5  | MET |
| 3. Gate stops out-of-corpus questions |4 of 5|5 of 5|5 of 5| 5 of 5  |MET|
| 4.At least 4 of 5 chunks contain a complete piece of information|4 of 5|  4 of 5|4 of 5|4 of 5|MET|
| 5.At least 4 of 5 test questions return the specific fact requested |4 of 5 |5 of 5 | 5 of 5 | 5 of 5  | 5 of 5 |MET

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

     Week 2 Unit 2 Run Logs

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer |4 of 5|5 of 5|5 of 5|5 of 5| MET |
| 2. Every answer names a source | 5 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 3. Gate stops out-of-corpus questions |4 of 5|5 of 5|5 of 5|5 of 5| MET |
| 4. At least 4 of 5 chunks contain a complete piece of information | 4 of 5 | Manual: 4 of 5 | Manual: 4 of 5 | Manual: 4 of 5 | MET |
| 5. At least 4 of 5 test questions return the specific fact requested | 4 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |

### Evidence from the Before Run

The results below are from `results/run_2026-10-04_0159_before.md`, produced by `run_eval.py::main`. I used one run from each question as evidence for the criteria.

**Criterion 1 — Retrieved chunk contains the answer**

Question: How long does an interlibrary loan request usually take?

```text
Requests through the interlibrary system take about a week (Source: admin_library_holds.txt).

**Criterion 2 — Every answer names a source**

Question: When do students declare a major?

```text
Students declare a major at the end of their second semester, or later if needed.

Source: admin_declaring_a_major.txt
```

The answer includes the source document.

**Criterion 3 — Gate stops out-of-corpus questions**

Question: How do I write a for loop in Rust?

```text
refused (best distance 0.896)
```

The gate refused the question because it was outside the campus-life information in the corpus.

**Criterion 3 — Gate stops out-of-corpus questions**

Question: How do I write a for loop in Rust?

```text
refused (best distance 0.896)
```

The gate refused the question because it was outside the campus-life information in the corpus.

**Criterion 4 — At least 4 of 5 chunks contain a complete piece of information**

I checked five chunks manually. Four of the five contained a complete piece of information without needing another chunk, so this criterion met the target of 4 of 5.

**Criterion 5 — At least 4 of 5 test questions return the specific fact requested**

Question: How many credit hours are required for graduation?

```text id="j5j2mb"
120 credit hours are required for graduation.

Source: admin_graduation_requirements.txt
```

The answer gives the specific number the question asked for.



## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunk contains the answer |MET  |All five test questions retrieved information containing the fact needed to answer the question, exceeding the target of 4 of 5.  |
| 2 |Every answer names a source  |MET | All five generated answers named a source document, meeting the target of 5 of 5.  |
| 3 | Gate stops out-of-corpus questions |MET | The gate refused all 5 out of scope questions, exceeding the target of 4 of 5. |
| 4 |At least 4 of 5 chunks contain a complete piece of information  | MET |My chunking review showed that at least 4 of the 5 checked chunks contained a complete piece of information without needing another chunk.  |
| 5 |At least 4 0f 5 test questions return the specific fact requested | MET | All five test questions returned the specific fact requested, exceeding the target of 4 of 5 |


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

No criteria were missed in the before evaluation. The retrieval, generation, and relevance gate all met the targets I set. The five in-scope questions consistently retrieved the needed information, the generated answers named their sources, and the gate refused all five out-of-scope questions. Because there were no misses to diagnose, I did not identify a single failing stage that required correction.

Unit 2 Milestone 3 Diagnoses

I did not miss any of the five criteria in the before test.  All five met the goals I set in Unit 1.  The questions were able to find the information needed, the answers included the source, and the system stopped questions that were not related to the campus-life information.  Since I did not miss any criteria, I think Criterion 1 could have been a little harder.  I would make the target stricter by requiring the top result to contain the information needed to answer all 5 questions. This would give me a better way to test if system is finding the right information. 


## The Improvement

**What I changed:** I added metadata filtering to retrieval using the document source field.  The search() function now accepts an optional source filter, and the retrieve command supports the --source option.  I tested the same question with and without the filter.  Without the filter, five documents were retrieved; with the filter set to admin_declaring_a_major.txt, only that document was returned.

**Why I picked it:** I picked metadata filtering because the documents already had source metadata, so I could add a useful retrieval control without changing the embedding model or adding another dependency.  It also gives the user a way to narrow retrieval to a specific source document when needed. 

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

Improvement Unit 2 improvement Part 2

*What I changed:***

I added conversational memory so the system can remember the question that came before it. This allows a second question to build on the first question instead of treating it as a completely new question. I will test this by asking a first question and then asking a follow-up question that depends on the first question.

**Why I picked it:**

I picked conversational memory because Criterion 1 could have been a little harder. My original test showed that the system could find the information needed for the questions, but I wanted to test how well it could handle questions that depend on previous information. This improvement gives me another way to test whether the system can understand what the user is asking in a conversation.

### Before Test Unit 2 Part 2

*What I changed:***
I added conversational memory to the interactive question mode. The system now keeps the previous question and uses it when the user asks a follow-up question. This allows the second question to use information from the first question instead of treating it as a completely new question.


**Why I picked it:**
I tested the system with two questions. First I asked, “When do students declare a major?” and the system found the correct source. I then asked, “What about if I need more time?” The system did not remember the first question and said it did not have enough information. This showed that the system was treating the second question as a new question instead of a follow-up.

## After the test Unit 2 Part 2

### After Test

I tested the same two questions again after adding conversational memory. First I asked, “When do students declare a major?” and the system found the correct source. I then asked, “What about if I need more time?” This time the system understood that the second question was a follow-up and answered that students can declare later if they need more time. It also retrieved `admin_declaring_a_major.txt`.

### Before vs. After

| Test                                                | Before                                                                     | After                                                                                                  |
| --------------------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| First question: “When do students declare a major?” | Correct answer and source                                                  | Correct answer and source                                                                              |
| Follow-up: “What about if I need more time?”        | Did not understand the follow-up and said there was not enough information | Correctly understood the follow-up and answered that students can declare later if they need more time |

**Result:** Before the improvement, the follow-up question did not work. After adding conversational memory, the follow-up worked and returned the correct information from `admin_declaring_a_major.txt`.



### Run Log — After
<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |5 of 5  |5 of 5  |5 of 5  |MET |
| 2. Every answer names a source | 5 of 5 | 5 of 5 | 5 of 5  |5 of 5  |MET  |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5 of 5 |5 of 5 |5 of 5  | MET |
| 4.At least 4 of 5 chunks contain a complete piece of information |4 of 5 |Use your manual chunk review |Use your manual chunk review |Use your manual chunk review |MET if review confirms |
| 5.At least 4 of 5 test questions return the specific fact requested |4 of 5 |5 of 5 |5 of 5 |5 of 5 |MET |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

     The metadata filter worked the way I expected. Without the filter, the question returned five different documents. With the filter, it only returned the document I selected. The before and after results were the same because my evaluation did not use the new filter. The system still answered all five questions correctly and rejected all five questions that were outside the campus information. The filter gives me more control over which document is used, but it did not change the results of my regular evaluation.


## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

     One thing I still need to work on is automatic scoring. I have not created the `scorer.py` file yet, so I had to look at the answers myself to decide if they met my criteria.I also only tested five questions. The results were consistent, but testing more questions would give me a better idea of how well the system works. I stopped here because the main goal for this milestone was to add and test the metadata filtering feature.

     Unit 2 Part 2

     ## What’s Still Broken

One thing I still need to work on is automatic scoring. I have not created the `scorer.py` file yet, so I had to look at the answers myself to decide if they met my criteria.  I also only tested a small number of questions. The conversational memory test worked, but testing more follow-up questions would give me a better idea of how well the system handles different conversations.


## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->

     I would make some of my criteria more specific. For example, instead of just checking if the retrieved chunk is related to the question, I would check if it actually contains the information needed to answer the question. I would also test more questions instead of only five. This would give me more information about how well my system works with different types of questions. I would keep my criteria about giving the correct answer and checking the quality of the chunks because I think those are important parts of the project.

