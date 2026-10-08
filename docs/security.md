# Security Considerations

## Authoritative server hardening

- Zone transfers restricted by `allow-transfer` ACL — only `10.26.216.144`
  (Clone) may pull from Main, and vice versa.
- Recursion is disabled on authoritative-only zones. Where recursion is
  enabled (Main), `allow-recursion` is restricted to `localhost` and
  `10.26.216.0/24`.
- `dnssec-validation no` in `named.conf.options` because the private root
  zone has no chain of trust to the public root.

## DNSSEC (future work)

DNSSEC signing of `ozy.cns` and `vic.cns` can be added with
`dnssec-policy default;` on each master. This would:

- Generate KSK + ZSK
- Sign all RRsets in the zone
- Publish DNSKEY at the zone apex
- Require the parent zone (`cns`) to publish a DS record

Deferred for now to keep the topology simple.

## Transfer security

AXFR between Main and Clone uses unencrypted TCP port 53. For production,
this should be wrapped in TLS (XFR-over-TLS, RFC 9103). For a private lab,
the security boundary is the internal subnet.

## Access control

- Only `10.26.216.0/24` clients can query the tree.
- Root zone contains no `forwarders` — all queries terminate within
  the internal tree.
