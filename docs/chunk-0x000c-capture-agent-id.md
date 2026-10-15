# Chunk 0x000c — capture agent ID (legacy) and 0x003e (uint32)

This document records the interoperability agreement from
[issue #2](https://github.com/sipcapture/HEP/issues/2) and supersedes the REV_37 table row for
chunk **0x000c** where it lists payload type **uint32** only.

## Background

Many HEP3 emitters (for example early **hepipe** and **captagent** builds) place the capture
agent identifier in chunk **0x000c** using a **four-octet chunk payload**, but encode the
numeric ID with **`htons()` semantics** (16-bit network byte order in the first two octets, with
the remaining octets zero). Example for agent ID `2001` (`0x07D1`):

```text
00 00 00 0c 00 0a 07 d1 00 00
```

Receivers that interpret all four octets as **`htonl()` / uint32** without compatibility logic
mis-identify the agent (for example reading `0` instead of `2001`).

Emitters that correctly use **`htonl()`** on a uint32 (for example **heplify** and current
**captagent** `transport_hep.c`) send IDs such as `2001` as `00 00 07 d1`.

## Legacy chunk 0x000c (required for backward compatibility)

| Field | Value |
|-------|--------|
| Vendor ID | `0x0000` |
| Type ID | `0x000c` |
| Payload length | 4 octets (chunk length field = `0x000a`) |

**On the wire:** treat the payload as a **uint16 capture agent ID in network byte order** stored
in the **first two octets**; the **last two octets MUST be zero** on send and SHOULD be ignored
on receive.

**Receivers** MUST decode legacy **0x000c** using this rule when chunk **0x003e** is absent.

**Senders** SHOULD continue to include legacy **0x000c** (with the uint16-compatible encoding
above) so older collectors remain functional.

## Canonical chunk 0x003e — capture agent ID (uint32)

New implementations SHOULD also send chunk **0x003e** when the agent ID does not fit uint16 or
when full uint32 range is required.

| Field | Value |
|-------|--------|
| Vendor ID | `0x0000` |
| Type ID | `0x003e` |
| Payload type | **uint32** (network byte order, `htonl`) |
| Chunk length field | `0x000a` (6 + 4) |

**Receivers** that support **0x003e** MUST use its value as the capture agent ID when present,
and MAY ignore **0x000c** for the numeric ID.

**Senders** SHOULD populate **0x003e** with `htonl(agent_id)` and keep **0x000c** as above for
transition.

## String agent identity

Chunk **0x0013** (capture agent name / node name) remains the preferred human-readable agent
identifier and is unchanged.
