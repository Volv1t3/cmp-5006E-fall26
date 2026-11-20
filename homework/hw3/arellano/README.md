# Homework 3 - AI Application Red Team

## Group members

- Isabella Tulcan Jaya - 00329994
- Martin Montero Torres - 00328595
- Santiago Arellano Jaramillo - 00328370

Run [hw3_ai_redteam.ipynb](hw3_ai_redteam.ipynb) from this directory using a
Python 3.10+ Jupyter kernel. It starts the course's local `vuln-llm` target
through `seclab.targets` unless `VULN_LLM_BASE` already names a loopback target.

Before the first container-based run, build the local image from the course root:

```zsh
docker build -t seclab/vuln-llm:local labs/vuln-llm
```

For a local Ollama-backed run, start Ollama and ensure the selected model exists:

```zsh
ollama serve
ollama pull qwen2.5:3b
```

The notebook uses `seclab.llm` to record local-model availability and the target
uses its local Ollama backend when reachable. If it reports `backend: mock`, the
attack logic remains runnable but its five trials are deterministic demonstrations,
not a measurement of model variability.

Run all cells in order. The notebook writes execution evidence to `artifacts/`:

- `hw3_redteam_results.json`
- `hw3_redteam_scorecard.csv`

Part A writes isolated audit evidence to `evidence/`:

- `part-a-requests/*.xml`: one XML document per local HTTP request, containing
  the request and its paired response.
- `part-a-findings.xml`: the Part-A reliability and oracle summary, with
  references to its request/response files.
- `part-a-findings.csv`: the Part-A finding rows for spreadsheet or
  statistical analysis.

Part B creates a separate evidence set and never appends to or replaces Part A:

- `path-b-requests/*.xml`: one XML document per local Part-B request, with its
  paired response and a phase such as `B.1-model-level-defense`.
- `part-b-findings.xml`: the Part-B filter, bypass, and containment summary.
- `part-b-findings.csv`: the same Part-B finding rows for data analysis.

All requests and the poisoned document server are restricted to `127.0.0.1` or
`localhost`. See [AI_LOG.md](AI_LOG.md) for the use of AI assistance.
