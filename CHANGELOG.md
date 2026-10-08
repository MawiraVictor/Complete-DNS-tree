# Changelog

All notable changes to the DNS tree project.

## [0.1.0] - 2026-10-08

### Added

- Initial BIND9 hierarchy: root zone, `cns` TLD, `ozy.cns`, `vic.cns`
- Third-level delegation: `eng.ozy.cns`
- Reverse zone: `216.26.10.in-addr.arpa`
- Master/slave replication with AXFR and NOTIFY
- `dig +trace` verification
- Packet capture evidence via tcpdump

### Changed

- Migrated all zones from 10.132.24.0/24 to 10.26.216.0/24

### Fixed

- Stale slave cache resolved via `rndc retransfer`
- Reverse zone filename and `named.conf.local` reference

### Infrastructure

- Main (10.26.216.236): master for `.`, `cns`, `ozy.cns`, `eng.ozy.cns`, reverse
- Clone (10.26.216.144): master for `vic.cns`, slave for all of the above
