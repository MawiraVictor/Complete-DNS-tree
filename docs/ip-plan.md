# IP Plan

| Hostname | IP | Role |
|----------|-----|------|
| ns1.cns / mail.ozy.cns | 10.26.216.236 | Root + TLD + ozy + eng master; vic slave |
| ns2.cns / vic.vic.cns | 10.26.216.144 | vic.cns master; slave for root, cns, ozy, eng |
| sqlslv2.vic.cns | 10.26.216.150 | MariaDB slave (not part of DNS tree) |

## Network

- Subnet: 10.26.216.0/24
- Gateway: 10.26.216.255
- Nameservers: 10.26.216.236, 10.26.216.144
- Reverse zone: 216.26.10.in-addr.arpa
