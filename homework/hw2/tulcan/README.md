# Homework 2 — Web Attack & Defend

## Group members

- Isabella Tulcan Jaya — 00329994
- Martin Montero Torres — 00328595
- Santiago Arellano Jaramillo — 00328370

## What to run

The implementation and its explanatory Markdown are in
[`hw2_web_attack_defend.ipynb`](hw2_web_attack_defend.ipynb). It contains:

- Part A: local DVWA-at-Medium payloads and sound oracles for SQLi, reflected
  XSS, and command injection.
- Part B: WAF coverage, bypasses, benign-traffic false positives, and the
  structural-fix comparison against DVWA's Impossible level.
- Part C: a Semgrep-versus-local-Ollama (`qwen2.5:3b`) duel against the readable
  `vuln-web` source and its independent hand-built ground truth.

All targets must be local and authorized. The notebook refuses a DVWA URL other
than `127.0.0.1` or `localhost`.

## Prerequisites

- Python 3.10 or later (the notebook was prepared for Python 3.15).
- Jupyter Lab/Notebook or VS Code with a Python kernel.
- Docker Desktop running and an authorized local DVWA instance configured at
  **Medium**. The notebook defaults to `http://127.0.0.1:60281`; override it
  with `DVWA_BASE` if Docker assigns another local port.
- Ollama serving locally with the model used for Part C:

  ```sh
  ollama serve
  ollama pull qwen2.5:3b
  ```

- Semgrep for the classical-scanner arm of Part C:

  ```sh
  python3.15 -m pip install semgrep
  ```

The notebook imports `pandas` for result presentation. Install it in the same
kernel if it is not already available.

## Run the notebook

From the repository root, set only local configuration. Do not commit passwords.

```sh
cd homework/hw2/tulcan
export DVWA_BASE='http://127.0.0.1:60281'
export DVWA_USERNAME='admin'
# Either set DVWA_PASSWORD in your local shell or let the notebook prompt for it.
jupyter lab hw2_web_attack_defend.ipynb
```

Select the Python 3.10+ kernel and run the cells in order. The notebook checks
that DVWA begins at Medium; its Impossible-level comparison blocks restore Medium
in `finally`, even if an assertion fails.

Part C makes two uncached local Ollama calls with different seeds. It writes the
raw model outputs, normalized findings, scores, and metrics to:

- `duel/part_c_results.json`
- `duel/part_c_metrics.csv`

Review those artifacts and the notebook's printed false positives, scanner miss,
and non-determinism section before writing the final report. They are evidence;
they should not be replaced by screenshots.

## Included source-of-truth files

- `ground_truth.json`: independently hand-verified findings for the `vuln-web`
  scan subject used in Part C.
- `benign_traffic.json`: legitimate inputs used to measure Part-B WAF false
  positives.
- `verify_fixtures.py`: instructor fixture check for the local `vuln-web` setup. Run `python verify_fixtures.py` from this directory.
- `AI_LOG.md`: disclosure of AI assistance used while preparing this submission.

## Windows PowerShell

From the repository root:

```powershell
cd homework/hw2/tulcan
$env:DVWA_BASE = "http://127.0.0.1:60281"
$env:DVWA_USERNAME = "admin"
jupyter lab hw2_web_attack_defend.ipynb
```

## Evidence provenance

This group submission was imported from Santiago's branch
homework/hw-2-arellano, commit 65cee0f. The saved notebook outputs and
duel artifacts come from his local execution; absolute macOS paths in those
outputs record that execution. They have not been relabeled as a Windows run.

## Local preparation checks

The fixture verifier passed for all three vulnerabilities, the safe endpoint,
and the benign corpus. All 20 notebook code cells passed Python syntax parsing.
The scan source SHA-256 matches the committed duel evidence after normalizing
line endings. The full DVWA/Ollama/Semgrep experiment was not rerun here.

## Submission map

- [attack/](attack/README.md): three Medium-level findings and archived oracles.
- [defend/](defend/README.md): WAF, original evidence, standalone parameterized
  fix, three same-intent SQLi mutations, and measured CSVs.
- [duel/](duel/README.md): two recorded model reviews, scanner metrics, limitations.
- [honesty.md](honesty.md): explicit limitations and fixture provenance.
- [AI_LOG.md](AI_LOG.md): assistance disclosure.

## Revision and remaining execution requirement

The revised notebook clears old outputs to avoid attributing them to changed
code. Original outputs remain in the archived attack/defense reports and duel
artifacts. It now rejects request/oracle errors and tests three SQLi bypasses
against DVWA, then replays all four SQLi inputs at Impossible.

The supplemental local SQLite experiment is independently executable and has
its own CSVs. It is not a substitute for a fresh DVWA run. Before claiming full
strict-rubric compliance, run the revised notebook against local DVWA and confirm
the three SQLi mutations. The recorded duel had no hallucinations; report that
honestly. Ground truth originated in the instructor fixtures and was reviewed
retrospectively; a claim of group construction before scanning would be false.
