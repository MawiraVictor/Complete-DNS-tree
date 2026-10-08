# Testing Methodology

## Zone validation

Before every reload:

- `named-checkconf` — validates the BIND configuration
- `named-checkzone <zone> /etc/bind/db.<zone>` — validates each zone file

## Query validation

For every new record or zone cut:

- `dig @127.0.0.1 <name> <type>` — direct query to the master
- `dig @<slave> <name> <type>` — verify slave has transferred the update
- `dig +trace <name>` — verify the delegation chain is intact

## Transfer validation

- `rndc retransfer <zone>` forces a fresh AXFR
- `tcpdump -i any -n 'tcp port 53'` captures the transfer on the wire
- `journalctl -u named` shows `Transfer completed` lines with record counts

## Reverse DNS validation

- `dig -x <ip>` — verifies PTR records

## Acceptance criteria

A zone change is considered deployed when:

1. The master accepts the new zone file (`named-checkzone` returns OK)
2. The master serves the new record (`dig @127.0.0.1` returns it)
3. Both slaves have transferred (`journalctl` shows `Transfer completed`)
4. A client on a different VM sees the new record via its local resolver
