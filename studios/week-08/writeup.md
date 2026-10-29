# Week 8 Control Scorecard

| Attack | Trusted name | Substituted artifact | Pin / control | Axis 2 guarantee |
|---|---|---|---|---|
| Dependency confusion | Package name `acme-auth` | Attacker's public package v9.9.9 | Lockfile with exact version, SHA-256 hash, and internal source scope | Only the exact vetted package artifact is accepted. |
| Transitive backdoor (XZ) | “It's just a dependency” | Compromised `xz-utils` code pulled in by `acme-auth` | Enumerate the full dependency tree in an SBOM; verify provenance and pin approved artifacts | The complete inventory makes hidden transitive artifacts assessable; provenance and pins constrain what is trusted. |
| `alg=none` JWT | Token's `alg` header | Unsigned token claiming `role: admin` | Pin `HS256` server-side and verify the signature with the server key | Only a token signed with the expected algorithm and key is accepted. |

**Shared guarantee (axis 2):** only the exact vetted artifact is trusted, under a key or list controlled by us. Names and self-descriptions alone do not establish identity.
