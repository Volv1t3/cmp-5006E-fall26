# Part B — Negative and positive models

The notebook contains the original DVWA experiment. Its saved results are in
[recorded_results.txt](recorded_results.txt). It measures initial WAF coverage
3/3, one bypass for each of three injection classes, and false positives 2/26
(7.69%). One blocked legitimate request is `drop table tennis lessons for beginners`.

The original three bypasses are across different classes. To demonstrate three
same-intent variants for **one** vulnerability, [evaluate.py](evaluate.py) adds
a separate, fully local numeric-ID SQLi experiment:

```sh
python homework/hw2/tulcan/defend/evaluate.py
```

It applies the notebook's WAF rules before the vulnerable sink and checks three
passing mutations (`1/**/OR/**/1=1`, `1 OR TRUE`, `1 OR 2>1`) against a private-row
canary, with three trials each. It also supplies an actual positive fix:

```python
db.execute('SELECT id, secret FROM users WHERE id = ?', (value,))
```

All four SQLi payloads are replayed against the fix, and an ordinary lookup must
still return its expected row. Exceptions terminate evaluation; they cannot count
as successful defense. The script writes [sqli_results.csv](sqli_results.csv)
and [benign_results.csv](benign_results.csv).

**Guarantee:** when this SQL statement is executed using SQLite parameter binding,
the input supplies one value and cannot change the statement's SQL structure.
This does not guarantee authorization or protect other string-built queries.
The WAF only matches known syntax and cannot give this guarantee.

**Scope distinction:** this added experiment runs against SQLite in-process. It
does not prove the two new mutations work against DVWA Medium. The notebook also
contains these extra DVWA SQLi checks for the next full run. The original B2
evidence uses DVWA's supplied Impossible implementations, not a group-authored
patch to DVWA. Recorded original results show 0/6 successful attack/bypass
payloads at Impossible and 3/3 functional benign controls.
