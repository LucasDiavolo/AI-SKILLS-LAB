# Validity checklist for original research (Track A)

Contents: 1 Claims and evidence · 2 Data and leakage · 3 Baselines and
comparisons · 4 Statistics · 5 Generalization · 6 Measurement and design ·
7 Reproducibility · 8 Reporting and integrity

For each item answer: **Pass / Concern / Fail / Cannot assess**, with a page reference.
Skip items that do not apply, and say they were skipped.

## 1. Claims and evidence
- Does each claim in the ledger have a result that directly tests it?
- Is the claim's strength matched to the evidence (causal wording from
  correlational data, "state of the art" from one dataset)?
- Do the abstract and conclusion promise more than the results section shows?
- Are negative or null results reported, or only favorable ones?
- Do the text numbers match the tables and figures?

## 2. Data and leakage
- Is the sample or dataset described well enough to judge representativeness?
- Are inclusion and exclusion rules stated, and applied before looking at outcomes?
- Is there a clean separation of train, validation, and test data?
- Could test information reach training through preprocessing, normalization,
  feature selection, tuning on the test set, or duplicated or near-duplicate items?
- Could the benchmark or test data overlap with pretraining data
  (for large pretrained models)?
- Are time-ordered data split by time rather than randomly?
- Are labels reliable (annotator agreement, label source, noise)?
- Is there missing-data handling, and could it bias results?

## 3. Baselines and comparisons
- Are baselines current, strong, and relevant, or weak and outdated?
- Were baselines tuned with the same effort and budget as the proposed method?
- Are compute, data, and parameter budgets comparable?
- Are baseline numbers reproduced by the authors or copied from other papers
  with different settings?
- Is there an ablation that isolates which component causes the gain?
- Does a trivial or simple baseline exist that was left out?

## 4. Statistics
- Sample size or number of runs adequate? Is power discussed?
- Variance reported across seeds, folds, or replicates (not a single run)?
- Confidence intervals or tests present, and are they the right ones?
- Effect size given, not only p-values?
- Multiple comparisons or many hypotheses handled?
- Signs of selective analysis: unexplained subgroups, outcome switching,
  flexible stopping, results shown only for the best configuration?
- Is a small improvement within plausible noise?
- Are the assumptions of the tests plausible?

## 5. Generalization
- Evaluated on more than one dataset, population, or setting?
- Out-of-distribution or robustness tests included?
- Does the conclusion extend beyond the sampled population or conditions?
- Is real-world feasibility (cost, latency, deployment constraints) addressed
  where the paper claims practical value?

## 6. Measurement and design
- Do the metrics measure the construct the paper claims to improve?
- Are metrics chosen after seeing results, or are alternatives reported?
- For experiments: randomization, blinding, control group, manipulation check.
- For observational work: confounders measured and handled; reverse causation
  and selection effects considered.
- For human or model-graded evaluation: rater count, agreement, and rater
  independence from the method's authors.
- For theory: are assumptions realistic, and is the proof complete and checkable?

## 7. Reproducibility
- Code, data, trained models, and configuration released or available?
- Hyperparameters, software versions, hardware, and random seeds stated?
- Is the full pipeline described, including preprocessing and evaluation scripts?
- Is a preregistration or protocol referenced?
- List each `[NOT REPORTED]` item that blocks replication.

## 8. Reporting and integrity
- Funding sources and conflicts of interest disclosed, and could they bear
  on the result?
- Ethics approval and consent stated where human or animal subjects are involved?
- Limitations section honest and specific, or generic?
- Any internal inconsistencies (sample sizes that change, impossible values,
  mismatched figure captions)?
- Reporting standard followed where one exists for the design
  (for example CONSORT for trials, STROBE for observational studies).
  Name the standard only if the paper cites it or the design clearly matches.

## Severity hints
- **Critical:** test leakage, outcome unsupported by any shown result,
  confound that fully explains the effect, results from a single run
  presented as general.
- **Major:** weak or untuned baselines, no variance reporting, a conclusion
  that extends well beyond the data, unreported key settings.
- **Minor:** missing code link, small reporting inconsistencies, unclear wording.