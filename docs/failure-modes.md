# Failure Modes and Recovery

## Master (Main, 10.26.216.236) goes down

- Clone still serves `vic.cns` as master and `ozy.cns`, `cns`, `.` as slave.
- Clients querying Clone still resolve everything.
- New writes to `ozy.cns` cannot happen until Main returns.
- On recovery: `systemctl start bind9` resumes the master role.

## Slave (Clone, 10.26.216.144) goes down

- Main is unaffected; still master for `.`, `cns`, `ozy.cns`, `eng.ozy.cns`.
- Main is slave for `vic.cns` — cached copy still serves queries.
- No new `vic.cns` updates until Clone returns.

## Zone transfer failure

Symptom: `journalctl -u named` shows `transfer of '<zone>' failed` or
stale serial.

Recovery:

1. `named-checkconf` on both ends
2. Check `allow-transfer` ACLs match the other server's IP
3. `rndc retransfer <zone>` to force a fresh pull
4. If stuck, delete cached file in `/var/cache/bind/` and restart BIND

## Stale records

If a slave has an old serial, `rndc status` shows `Transfer failed`.
Force `rndc retransfer <zone>`.
