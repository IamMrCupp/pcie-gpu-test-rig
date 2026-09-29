# pcie-gpu-test-rig

A bench rig for powering a graphics card with no motherboard — a PCIe riser and the card's aux connectors, fed from a current-limited bench supply through a fused, switched, metered 12 V box. Put a dead card on it and in thirty seconds you know whether it draws nothing, idles like a healthy card, or drags the supply into current limit.

![Wiring schematic, rev C](wiring/pcie_rig_power.svg)

## What's here

| Path | What |
|---|---|
| [`wiring/pcie_rig_power.kicad_sch`](wiring/pcie_rig_power.kicad_sch) | The schematic. KiCad 10, ERC clean with every severity on — CI re-checks it on every push. |
| [`wiring/pcie_rig_power.pdf`](wiring/pcie_rig_power.pdf) · [`.svg`](wiring/pcie_rig_power.svg) | Renders, regenerated from the schematic with `kicad-cli`. |
| [`WIRING.md`](WIRING.md) | The build: parts with sources, wire-by-wire list keyed to the schematic's nets, lead builds, build order, pre-power checks, limits. |

The printed enclosure — a 4×4 Clickfinity-footed box with the meter, switch, and probe post on the deck and the riser docked on top — lives in [3d-printer-models](https://github.com/IamMrCupp/3d-printer-models) as `pcie-rig-enclosure` ([in review](https://github.com/IamMrCupp/3d-printer-models/pull/165)), so it keeps the shared Gridfinity library and that repo's render checks. The wiring doesn't depend on it.

## How it works

**12 V IN → 8 A fuse → PZEM-031 meter → rocker → outputs.** Keyed XT60 for the riser and the card, banana pairs beside them for probing and plain-lead supplies, and a probe-ground post for the scope. The meter sits ahead of the switch, so you see 12.0 V on the box before you ever enable the card.

**The protection is the bench supply, not the box.** Set it to 12.0 V, OVP 12.6 V, and a 6 A current limit — the rig's working ceiling. The fuse is a backstop. Everything else in the path is overrated on purpose.

> **Never feed this from an ATX or server supply** — anything that can deliver tens of amps into a shorted card will. A current-limited bench supply is the whole point.

## What it tells you

| Reading | Usual meaning |
|---|---|
| About 0 A | Rails aren't coming up. Check the enable chain, and see *Caveats*. |
| Roughly 1–2.5 A | The card is idling. |
| Supply drops into current limit | A short or a stuck phase. Switch off, then find it with injection and a thermal camera. |

The idle range is a starting point from other people's builds, not a spec. Build your own table from known-good cards.

## Two wiring traps

Both are in [`WIRING.md`](WIRING.md) and on the schematic sheet, and both fail silently:

- **The meter's shunt is in the negative leg**, between its terminals 2 and 1. Land the input negative on the ground bus instead of terminal 2 and the current bypasses the shunt — the meter reads 0.00 A forever and a working card looks dead.
- **The rocker's load and LED pins must not swap.** Put the load on the LED pin and ground on the load pin, and the first flick is a dead short across the meter. Beep the pins before crimping.

## Caveats

- **PERST#.** On a bare riser the PCIe reset line isn't driven by a host. Most cards sequence their rails anyway; not every generation is guaranteed to. If a known-good card sits near 0 A, look there first.
- **This proves a card idles safely and nothing more.** A card that passes still needs a real system and a memory test before it goes back to anyone.

## Prior art

The idea isn't new. northwestrepair's *Super Mega Tester Pro XL* (2023) and GPU Solutions' custom GPU testing power supply (2026) build the same thing; this is my take on it, sized for my bench.

## License

MIT — see [LICENSE](LICENSE). The enclosure in 3d-printer-models is CC BY-NC 4.0.
