# Manual source review of ground truth

Review target: `labs/vuln-web/app/vulnweb_app.py`. This review records direct
inspection of the source during submission preparation. It was performed after
the existing tool results were available, so it cannot retroactively establish
a blinded, pre-scan group ground-truth construction.

| Key | Source reasoning | Oracle / counterexample |
|---|---|---|
| `sqli/do_login` | Both credentials enter a formatted SQL string before `DB.execute(query)` | Tautology returns the seeded admin secret |
| `xss/do_reflect` | `name` enters an HTML f-string without escaping | Script markup survives unescaped |
| `cmdi/do_ping` | `host` enters a command string without validation | Lab detector reports shell metacharacters; execution is simulated |
| clean `do_reflect_safe` | Uses `html.escape(name)` | Script tag becomes text |
| absent `broken-access-control` | No separate session/role/ownership enforcement workflow | Injection alone does not establish a separate access-control flaw |

The group retained the instructor's fixture keys because source inspection
supports them, not because a tool reported them. The fixture's original authorship
is the instructor's; it was not independently constructed by the group before
running the duel. `verify_fixtures.py` dynamically checks the three positive
cases, the safe endpoint, and benign corpus against the local teaching app.

For strict compliance with a requirement for a fresh pre-scan truth set, a new
experiment on a separately reviewed target is needed. Do not represent this
retrospective review as that experiment.
