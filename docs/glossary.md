# DNS Glossary

- **Zone** — A portion of the DNS namespace administered by a single authority.
- **SOA** — Start of Authority — first record in every zone, defines serial, refresh, retry, expire, negative TTL.
- **NS** — Name Server record — declares the authoritative nameservers for a zone.
- **A / AAAA** — IPv4 / IPv6 host address records.
- **PTR** — Pointer — reverse zone record mapping IP → hostname.
- **CNAME** — Canonical name — alias for another name.
- **MX** — Mail exchange — where mail for a domain is delivered.
- **TXT** — Text — arbitrary text, used for SPF, DKIM, verification.
- **Delegation** — Parent zone refers queries for a child zone to the child's nameservers via NS records.
- **Glue record** — A/AAAA record in the parent zone providing the IP of a child-zone nameserver whose name is inside the child zone.
- **AXFR** — Full zone transfer — TCP-based replication of an entire zone.
- **IXFR** — Incremental zone transfer — only changes since a known serial.
- **NOTIFY** — Master's signal to slaves that a zone has changed.
- **Serial** — Monotonically increasing number in SOA, used to detect updates.
- **Root zone** — Top of the DNS hierarchy, denoted by `.`.
- **TLD** — Top-Level Domain — immediately below root (e.g., `com`, `cns`).
- **FQDN** — Fully Qualified Domain Name — ends with a dot, absolute from root.
- **Recursion** — A resolver's behavior of querying other servers to answer a query.
