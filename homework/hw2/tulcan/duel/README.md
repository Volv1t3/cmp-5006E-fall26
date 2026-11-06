# Part C — Semgrep versus Ollama

The notebook's Part C is the executable workflow. The committed
[raw results](part_c_results.json) include both model responses, configuration,
normalized findings, scores and target source hash. [Metrics](part_c_metrics.csv):

| Tool | Precision | Recall | F1 |
|---|---:|---:|---:|
| Semgrep, custom rules | 1.000 | 0.667 | 0.800 |
| Ollama qwen2.5:3b, seed 11 | 1.000 | 1.000 | 1.000 |
| Ollama qwen2.5:3b, seed 29 | 1.000 | 1.000 | 1.000 |

The scanner misses SQLi in `do_login`: its deliberately narrow rule looks for an
f-string directly inside `execute`, while the application builds a query variable
first. This is a limitation of **our custom rules**, not a conclusion about
Semgrep's standard security rules or scanners in general.

**Hallucinations:** none were observed in either recorded run (zero false-positive
finding keys). There is no genuine example to name, and none has been invented.
The model's `confirmed` label is a model assertion, not dynamic confirmation.

**Non-determinism:** both calls use temperature 0.7, distinct seeds, and disabled
cache reads. Finding sets are identical (Jaccard 1.000); wording differs. Two
runs do not establish that the model is deterministic. Neither tool reports
Broken Access Control. The small target provides no separate session/role/
ownership policy to evaluate under that class.

Ground truth is documented in [ground_truth_review.md](ground_truth_review.md).
The scanner and model inspect vuln-web, while Parts A/B inspect DVWA: this is a
cross-target limitation, not a direct comparison against the attacked DVWA code.
