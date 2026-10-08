# Operations Runbook

## Common commands

### Master — check status
named-checkconf
rndc status
systemctl status bind9

text

### Force reload
named-checkzone ozy.cns /etc/bind/db.ozy.cns
systemctl reload bind9

text

### Force slave to re-transfer
rndc retransfer vic.cns
rndc retransfer ozy.cns

text

### View current serials
rndc zonestatus ozy.cns

text

### Capture live DNS traffic
tcpdump -i any -n port 53

text

## Adding a new record

1. Edit `/etc/bind/db.<zone>` on the master
2. Increment the SOA serial (YYYYMMDDNN format)
3. `named-checkzone <zone> /etc/bind/db.<zone>`
4. `systemctl reload bind9`
5. Watch slave transfer: `journalctl -u named -f`

## Adding a new host

1. Add the A record to the appropriate zone
2. Add the reverse PTR to `216.26.10.in-addr.arpa`
3. Increment both serials
4. Reload and verify

## Rollback

Keep a copy of the previous zone file:
cp /etc/bind/db.ozy.cns /etc/bind/db.ozy.cns.bak

text

To roll back:
mv /etc/bind/db.ozy.cns.bak /etc/bind/db.ozy.cns
systemctl reload bind9

text
