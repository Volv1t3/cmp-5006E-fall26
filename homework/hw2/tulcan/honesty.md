# Where our attack, defense, or comparison might be unfair.

1. **Ground-truth provenance.** We used the instructor's supplied fixtures.
   Submission preparation added a source review, but it occurred after the
   recorded duel. Independence from the evaluated tool outputs is supported by
   fixture provenance; a new group-authored pre-scan truth set was not produced.
2. **Unequal tool tuning.** Our Semgrep rules intentionally miss indirect SQL
   construction. The model sees source comments that label vulnerabilities and
   suggest fixes. The reported scores describe this teaching setup, not a fair
   general ranking of LLMs and production scanner rulesets.
3. **Small benign corpus.** The 26 inputs are supplied teaching examples, not
   sampled production traffic. The measured 7.69% false-positive rate must not
   be generalized to real workloads. All fields use the same WAF rules.
4. **Different targets.** Parts A/B attack DVWA; Part C reviews vuln-web. The
   supplemental positive-fix experiment uses SQLite. Its results cannot be
   relabeled as MySQL/DVWA evidence.
5. **Limited oracles.** The XSS checks verify dangerous unescaped markup, not
   observed browser execution. DVWA SQLi checks an additional known row instead
   of the course app's literal canary. Command injection in the duel target is
   simulated. These differences bound the claims being made.
6. **Supplied structural fix.** The original notebook switches to DVWA Impossible;
   the group did not implement that fix. The added parameterized SQLite path is
   group submission code, evaluated separately and clearly labeled.
7. **Reproducibility.** Original DVWA/Ollama outputs belong to Santiago's run.
   Subsequent notebook code changes require a new run; old outputs do not prove
   the modified code executed. Two LLM samples with identical findings do not
   establish determinism, and no observed hallucination has been fabricated.
8. **Remaining strict-rubric gap.** Three same-intent SQLi bypasses are tested in
   the supplemental SQLite lab. A fresh DVWA Medium run is still needed to
   confirm all three against the original target. New error checks ensure failed
   requests cannot count as a successful structural defense in that rerun.
