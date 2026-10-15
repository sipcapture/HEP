# HEP3 extended total packet length (> 65535 octets)

Proposal referenced from [issue #9](https://github.com/sipcapture/HEP/issues/9). It extends
[HEP3 Network Protocol Specification REV_37](HEP3_Network_Protocol_Specification_REV_37.pdf)
without changing the `HEP3` (`0x48455033`) identifier.

## Problem

The HEP3 header uses a **16-bit** total length (octets 4–5, network byte order). Valid sizes are
**6** through **65535**. Encapsulated signaling payloads (for example large HTTP/2 bodies inside
chunk **0x000f**) can exceed this limit.

## Backward-compatible framing

### Packets of 65535 octets or less

Unchanged: octets 4–5 hold the total packet length (including the 6-octet header and all chunks).

### Packets larger than 65535 octets

| Octet offset | Size | Content |
|--------------|------|---------|
| 0–3 | 4 | `HEP3` (`0x48 0x45 0x50 0x33`) |
| 4–5 | 2 | `0xFFFF` (extended-length sentinel) |
| 6–9 | 4 | **uint32** total packet length, network byte order (minimum `65536`) |
| 10+ | — | Chunk payload (same TLV structure as REV_37) |

**Senders** MUST use the extended form when total size exceeds **65535**. They MUST NOT use
`0xFFFF` unless the true total length is **greater than 65535**.

**Receivers** that support this extension:

1. If bytes 4–5 are not `0xFFFF`, use them as the 16-bit total length (existing behavior).
2. If bytes 4–5 are `0xFFFF`, read the **uint32** at bytes 6–9 as the total length, then parse
   chunks starting at offset **10**.

**Receivers** without support treat `0xFFFF` as a conventional length (legacy behavior) and will
not correctly decode oversized frames; deploy extended senders only toward collectors that
advertise support.

## Scope and alternatives

This extension addresses **single-frame** size only. For very large mirrored traffic, duplicating
at the network tap may still be more efficient than HEP encapsulation, as discussed in the issue
thread.

Implementations may also use vendor-specific transports (for example protobuf ingest) where
appropriate; this document standardizes an in-band HEP3-compatible option.
