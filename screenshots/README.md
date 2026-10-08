# Screenshots

Verification screenshots for the DNS tree.

## 01-dig-trace.png
`dig +trace www.eng.ozy.cns @10.26.216.236` — walks the delegation chain.

## 02-wireshark-axfr.png
Wireshark capture of an AXFR zone transfer between Main and Clone.

## 03-reverse-ptr.png
`dig -x 10.26.216.236` — reverse DNS returning `mail.ozy.cns`.
