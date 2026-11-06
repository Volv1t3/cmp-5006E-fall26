# Part A — DVWA Medium

The primary executable is [the notebook](../hw2_web_attack_defend.ipynb),
Part A (cells 2–7, numbered from zero). Saved execution evidence is in
[recorded_results.txt](recorded_results.txt); it comes from Santiago's run.

| Class | Payload | Oracle | Saved successes |
|---|---|---|---|
| SQLi | `1 OR 1=1` | Additional synthetic row, `Surname: Smith`, absent for ID 1 | 3/3 |
| XSS | `<ScRiPt>window.__HW2_XSS__=1</ScRiPt>` | Unique script survives unescaped in the reflected sink | 3/3 |
| cmdi | `127.0.0.1 \| whoami` | `www-data` on its own line inside command output | 3/3 |

All three benign controls remained negative. The notebook checks Medium before
the attacks and restricts the configured target to loopback. XSS uses an HTML
reflection oracle; JavaScript execution was not independently measured in a browser.
SQLi uses a known extra row as a data-disclosure marker rather than vuln-web's
literal canary. These are DVWA-specific adaptations of the assignment oracles.

All three findings map to OWASP 2021 A03 (Injection). These observations do not
establish a separate A01 finding: no test demonstrates a role or ownership policy
violation independent of the injection. DVWA itself has authentication; this
conclusion must not be read as saying DVWA has no authentication code.
