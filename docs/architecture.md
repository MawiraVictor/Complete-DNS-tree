
<img width="307" height="152" alt="image" src="https://github.com/user-attachments/assets/fe1aef2c-866d-4042-a141-c9ba2d6082b9" />

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
