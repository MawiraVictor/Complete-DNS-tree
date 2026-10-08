# DNS Tree Architecture

## Hierarchy
. ROOT
│
└── cns TLD
│
├── ozy.cns
│ └── eng.ozy.cns
│
└── vic.cns

text

## Delegations

- `.` delegates `cns` → ns1.cns, ns2.cns
- `cns` delegates `ozy.cns` → ns1.ozy.cns, ns2.ozy.cns
- `cns` delegates `vic.cns` → ns1.vic.cns, ns2.vic.cns
- `ozy.cns` delegates `eng.ozy.cns` → ns1.eng.ozy.cns, ns2.eng.ozy.cns

## Replication

- Main is master for `.`, `cns`, `ozy.cns`, `eng.ozy.cns`, reverse
- Clone is slave for those (AXFR + NOTIFY)
- Clone is master for `vic.cns`; Main is slave for it
