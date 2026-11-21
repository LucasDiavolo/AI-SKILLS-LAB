---
name: paragraph-writing-v2
description: Write one formal academic paragraph in Indonesian (EYD V) grounded only in uploaded PDF articles, with page-level citations. Use when the user uploads papers and asks for a paragraph on a specific topic, for example "write a paragraph about the effect of X on Y from this article". The user must state the topic; if missing, ask before writing. The skill analyzes the sources itself, checks every number and page against the PDF, imitates the style of the user's thesis or article reference files when provided, and returns one paragraph of 3 to 8 sentences (125 to 531 words). Do not use for full article analysis, paraphrasing, bibliography formatting, or keyword search.
metadata:
  version: 2.1
  category: paragraph-writing-v2
  author: Lucas il Diavolo
---

# PDF-Grounded Paragraph Writing

Output: one paragraph in formal Indonesian (EYD V), 3 to 8 sentences,
125 to 531 words, every factual sentence sourced from the PDFs with a page
citation. This skill works on its own and needs no output from other skills.

## Step 1: Acquire sources (PDF only)

1. Read the PDFs from the conversation or `/mnt/user-data/uploads/`. If there is
   no PDF (only a link, DOI, or title), stop and ask for the PDF file.
2. Give each file one role:
   - **SOURCE:** an article that may be cited.
   - **STYLE REFERENCE:** a thesis or sample article from the user. Used only to
     imitate style. Never cited, never a source of facts.
   If the role is unclear, ask one question.
3. Label SOURCES S1, S2, and so on, in upload order.
4. Extract text with layout preserved (`pdftotext -layout` or `pdfplumber`).
   Use OCR for scanned PDFs. Read tables and figures from the actual page; never
   retype numbers from memory.
5. Record per SOURCE: authors (as printed), year, title, journal, DOI, and the
   offset between printed page number and PDF index. Write "tidak tercantum
   dalam PDF" for any field not printed.
6. If the text is unreadable or scrambled, ask for a better PDF before continuing.

## Step 2: Check the topic

1. The topic must come from the user. Never infer it from the title or abstract.
2. If the topic is missing or too broad ("write a paragraph from this article"),
   stop and ask one question: "What topic should the paragraph cover?"
3. If the request is to summarize the whole article, say that this is an article
   analysis task and ask for a narrower topic.
4. If the user supplies their own finding or statement, use it exactly as written.
   Never invent results, aims, or novelty claims on the user's behalf.
5. Restate the topic in one sentence as the anchor for the next steps.

## Step 3: Analyze sources and verify citations

This step is the skill's own analysis system. Work only on the parts of the
PDFs that touch the topic.

**3.1 Source analysis.** For each SOURCE, fill six fields:

| Field | Content |
|---|---|
| Type | original research or literature review (check title and methods) |
| Subject | species, sample, or scope of the study |
| Treatment or variable | what was given or measured, including dose and duration |
| Results related to topic | findings with numbers, units, and direction of change |
| Limitations | stated by the authors, or obvious from the design (single run, small sample, mixed treatments) |
| Location | page, table, or figure |

Special rule: in a review article, findings from cited studies are written as
secondary citations ("dikutip dalam"), not as the review authors' own findings.

**3.2 Claim-evidence map.** List the claims the paragraph needs, one per row,
then match each to evidence:

| Claim | SOURCE | Page | Exact number or statement | Limitation note |
|---|---|---|---|---|

**3.3 Verification.** Reopen the original page for every row and check: correct
page; same meaning and same hedging words; exact numbers and units; context
(subject and conditions) matches how the paragraph will use it; and whether it
is the authors' own finding or a cited one.

**3.4 Decision.** Each piece of evidence has only two statuses:
- **Used:** passes every check. Any limitation note must appear in the sentence.
- **Dropped:** fails any check, or cannot be confirmed from the PDF.

**3.5 Sufficiency.** If the Used evidence cannot cover the topic or cannot reach
125 words without padding, stop. Tell the user what the PDFs cover and ask for
more articles or a broader topic. Never fill gaps from outside knowledge.

## Step 4: Write and evaluate

**4.1 Write.**
- Structure: an opening sentence carrying the paragraph's idea, evidence with
  citation, interpretation, then a closing implication or limit. One idea per
  paragraph.
- Map every factual sentence to one evidence row before writing.
- Paraphrase fully. At most one direct quote per source, under 15 words.
- Word strength must match evidence strength: do not use "membuktikan" or causal
  verbs when the source reports only a correlation or a single trial.
- Interpretation sentences use words like "kemungkinan" or "dapat diduga" and
  carry no page citation.
- If a STYLE REFERENCE exists, follow its sentence length, structure, and
  citation density (see `references/paragraph-patterns.md`). Never copy its sentences.
- Language: formal, standard, EYD V, no "saya" or "kita". Citation and
  reference format follow `references/citation-rules.md`.

**4.2 Evaluate.** Check each item as Pass or Fail:
1. Every factual sentence matches one Used evidence row.
2. Numbers, units, and pages are identical to the PDF.
3. Meaning, hedging, and scope are not strengthened or shifted.
4. One paragraph, 3 to 8 sentences, 125 to 531 words (count including
   citations), no sentence over 55 words.
5. No invented results, aims, or facts, and no content from a STYLE REFERENCE.
6. Citation format is correct; secondary citations use "dikutip dalam".
7. EYD V is correct; no cliché phrases ("perlu dicatat bahwa", "di era modern
   ini", "memainkan peran penting").

**4.3 Fix.** Fix failed items, then recheck the whole list. Maximum two rounds.
If a sentence fails item 1, 2, 3, or 5, delete it. Never add material outside
the Used evidence.

## Step 5: Output

Read `assets/output-template.md` and follow its order. Show only:
1. **Paragraph**
2. **Verified citations** (sentence → SOURCE, page) plus a short note: dropped
   evidence with reasons, and sentence and word counts
3. **Reference list** (only sources actually cited)

Do not show drafts, the full map, or the analysis process. If the evidence
limits the paragraph (for example the source is only a review), say so in one sentence.



