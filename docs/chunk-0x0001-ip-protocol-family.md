# Chunk 0x0001 — IP protocol family

This note clarifies [issue #6](https://github.com/sipcapture/HEP/issues/6) for implementers reading
[HEP3 Network Protocol Specification REV_37](HEP3_Network_Protocol_Specification_REV_37.pdf).

## Values are POSIX address families, not IANA numbers

Chunk **0x0001** (`IP protocol family`) carries a single **uint8** value. HEP3 on-the-wire
values follow the **BSD/POSIX `AF_*` constants** used by capture agents on the host, **not**
the [IANA Address Family Numbers](https://www.iana.org/assignments/address-family-numbers/address-family-numbers.xhtml)
registry.

| uint8 value | Meaning | Typical constant (Linux) |
|-------------|---------|---------------------------|
| `2` | IPv4 | `AF_INET` |
| `10` | IPv6 | `AF_INET6` |

IANA assigns `1` to “IP (IP version 4)” and `2` to IPv6. **Do not** map IANA numbers into
chunk 0x0001 when building or parsing HEP3 packets; doing so will not interoperate with
existing Homer capture agents, Kamailio, Captagent, Heplify, hep-js, and related tools.

## Example packet annotation

The worked example in REV_37 includes:

```text
00 00 00 01 00 07 02    ; chunk 0x0001, length 7, payload 0x02
```

The comment `protocol family = 2 (IPv4)` is **correct for HEP3**: `0x02` is `AF_INET`, not IANA
value `1`.

When the family is IPv4 (`0x02`), source and destination addresses use chunks **0x0003** and
**0x0004**. When the family is IPv6 (`0x0a`), use chunks **0x0005** and **0x0006**.
