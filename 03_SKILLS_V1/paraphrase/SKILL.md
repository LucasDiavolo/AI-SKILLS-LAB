---
name: paraphrase
description: Rewrite a paragraph or text sentence by sentence without changing meaning, and without adding or removing sentences, in the voice of a sharp, professional graduate student. Output language matches the input (Indonesian or English). Use when the user sends text and asks to paraphrase, rewrite, reword, or "parafrasa". Numbers, citations, technical terms, and equations stay unchanged. Do not use for summarizing, shortening, expanding, translating, writing new paragraphs, or formatting references.
metadata:
  version: 1.1
  category: paraphrase
  author: Lucas il Diavolo
  license: Private modification
---

# Sentence-Faithful Paraphrasing

Output: the same text, rewritten. Same meaning, same number of sentences, same
order, written in the natural voice of a sharp, professional graduate student.
The skill works on its own.

## Step 1: Receive the text

1. Take the text from the message or an uploaded file. If there is no text,
   ask the user to send it.
2. Detect the language of the text. Write the output in that language. If the
   text mixes languages, use the language of the main body and leave quoted
   foreign terms as they are. Do not translate unless asked.
3. Number the sentences. A sentence ends at terminal punctuation; periods in
   abbreviations, decimals, and citations ("dkk.", "et al.", "hlm.", "3.5") do
   not end a sentence. Keep the count: N sentences in, N sentences out.
4. Mark everything that must stay unchanged: numbers and units, citations
   (author, year, page), technical terms, species and gene names, equations,
   proper names, and direct quotes.
5. If the user gives a target field or audience, note it. Otherwise assume
   formal academic writing.

## Step 2: Understand each sentence

For every sentence, write down internally:
- **Core idea:** the one claim, finding, or definition it carries.
- **Relation:** how it links to the previous sentence (adds, contrasts, causes,
  exemplifies, concludes).
- **Strength:** the hedging and certainty it expresses ("may", "significantly",
  "suggests", "dapat", "cenderung").
- **Scope:** who or what it applies to, and under what condition.

Do not write the paraphrase until all sentences are understood. If a sentence is
ambiguous, keep its ambiguity in the rewrite and flag it in the output.

## Step 3: Rewrite

Rewrite sentence by sentence.
- Each sentence stays one sentence, in the same position. Do not merge, split,
  add, or delete sentences.
- Change the structure, not just the words. Reorder clauses, switch between
  active and passive, move the condition or the result to the front, or change
  the main verb's framing. Synonym swapping alone is not a paraphrase.
- Keep the core idea, relation, strength, and scope exactly. Do not add
  interpretation, examples, or emphasis that is not in the original. Do not drop
  a hedge, and do not add one.
- Keep everything marked in Step 1 unchanged. Citations stay attached to the
  claim they support.
- Keep the original's logical connectors in meaning (contrast stays contrast),
  though the connecting word may change.
- Keep every technical term. Do not replace a precise term with a vaguer one.

## Step 4: Give it a human voice

Write as a sharp, professional student would: someone who knows the material and
writes with control, not with decoration.
- **Specific:** choose the concrete noun or verb over the abstract one.
- **Plain:** the simplest accurate wording; no inflated vocabulary.
- **Uneven rhythm:** mix short and long sentences within the paragraph. If the
  original is uniform, vary the internal structure without changing the sentence
  count.
- **Direct:** state the point first, then the qualification.
- **No filler:** no stock openers, no empty emphasis, no stacked hedges, no
  summary-style endings, no habitual "not only ... but also" or "tidak hanya ...
  tetapi juga". See `references/voice-guide.md` for the lists in both languages.
- **Level-headed:** not smarter, grander, or more confident than the original.
- Do not add deliberate typos, grammar errors, slang, or personal opinions to
  look human. The voice must come from precision and rhythm.
- Indonesian: formal, standard, EYD V, impersonal ("penelitian ini", "penulis"),
  no "saya" or "kita" unless the original has them.
- English: formal academic, standard spelling, keep the original's variant
  (US or UK).

## Step 5: Check

Mark each item Pass or Fail:
1. Sentence count and order are identical to the original.
2. Each rewritten sentence carries the same core idea, relation, strength, and
   scope as its original.
3. Nothing was added: no new claim, example, cause, or emphasis.
4. Nothing was dropped: no condition, hedge, number, or citation.
5. All protected items from Step 1 are unchanged.
6. Each sentence differs from the original in structure, not only in vocabulary,
   and no run of five or more words is copied unless it is a protected item.
7. No phrase from the filler lists; sentence lengths vary; language matches the input.

Fix any Fail and recheck the whole list. Maximum two rounds. If a sentence still
fails item 2, 3, or 4, return the closest faithful version and flag it.

## Step 6: Output

Read `assets/output-template.md` and follow it. Show:
1. **Paraphrase** (the rewritten text, same paragraph breaks as the original)
2. **Fidelity check** (one row per sentence: the core idea in a few words, and
   what changed structurally)
3. **Flags** (ambiguous sentences, or items that could not be changed without
   altering meaning; "none" if clean)

Do not show drafts. Do not comment on the quality of the original.