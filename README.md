# wic2005-w02 — a network described as data

WIC2005 Programmable Networks, Week 2. The network is described once, as data,
and that one description produces two outputs: a running Mininet network, and
this documentation.

## Files

| File | What it is |
|---|---|
| `topology.yaml` | The network description (YAML serialisation) |
| `topology.json` | The same description (JSON serialisation) |
| `build_topo.py` | Loads, validates and builds the description in Mininet |

## The network

One data model: two switches (`s1`, `s2`), four hosts (`h1`–`h4`), five links.
Addresses come from student ID block `10.50.0.0/16` and `fd00:0050::/32`.

## Wrap-up answers

**1. Data model vs serialisation.**
The *data model* is the structure: a list of switches, a list of hosts (each
with a name, an IPv4 and an IPv6 address), and a list of links. *Serialisation*
is how that structure is written down as text. `topology.yaml` and
`topology.json` are the same model; only the syntax differs. Converting between
them changed nothing about the model — it only lost the YAML comments, since
JSON has no comment syntax. Comments are part of one serialisation, not of the
model.

**2. Why validate in `check()` rather than with `pingall`.**
Two hosts with the same address still build, and `pingall` reported only 1
failure out of 12 — the network looked almost healthy. Which host answers
depends on which one replies to ARP first, so the fault is intermittent and
wastes time to diagnose. `check()` catches it before anything is built.

IPv6 noticed what IPv4 could not: Duplicate Address Detection. Before using a
new address an IPv6 host asks the network whether anyone already has it, and
marks its own address `dadfailed` if so. IPv4 has no built-in equivalent.

**3. What `git diff` gives you.**
A line-by-line record of what changed, when, and in which commit — plus the
ability to review it before it is applied and roll back to any earlier version.
A folder of files named `topology-v2-final` is just copies: no authorship, no
reason, no history, and no way to see exactly which lines moved.
