# Bill of materials

Everything you buy or print to build one rig. Quantities are for one box with both outputs fitted. Reference designators match the schematic and [WIRING.md](WIRING.md); the machine-generated list KiCad pulls from the schematic itself is [`wiring/pcie_rig_power_bom.csv`](wiring/pcie_rig_power_bom.csv), and CI fails if the two drift.

Prices move; links are what I bought from. Anything equivalent works if it matches the dimensions in the enclosure's README.

## Panel parts

| Ref | Qty | Part | Notes | Source |
|---|---|---|---|---|
| M1 | 1 | **Peacefair PZEM-031** DC meter, 8–100 V / 0–20 A, LCD, built-in shunt | housing 84.29 × 44.50, bezel 89 × 49, 24.45 deep. Four screw terminals | sold as HiLetgo, [B079JVGRSL](https://www.amazon.com/dp/B079JVGRSL) |
| SW1 | 1 | **Ampper** 20 mm round rocker, 12 V 20 A, 3-pin, illuminated dot | snap-in, body 20.87. Comes in a 10-pack | [B0BZPY5D9L](https://www.amazon.com/dp/B0BZPY5D9L) |
| F1 | 1 | **5×20 mm panel-mount fuse holder**, screw cap | thread 11.6, 26 long. From the fuse kit | Gebildet kit, [B07VT4VRW7](https://www.amazon.com/dp/B07VT4VRW7) |
| — | 1 + spares | **8 A fast-blow 5×20 glass fuse** | from the same kit (steps 5 → 8 A; 5 A blows in normal use) | same |
| J1 | 1 | **AMASS XT60E-M** panel-mount, male, pre-wired 12 AWG | captive nuts in the ears. Body 15.61 × 8.08, flange 27.21 × 12.07, ears 22.60 apart. One spare is handy | Amazon, sold in pairs |
| J3, J4 | 2 | **AMASS XT60E-F** panel-mount, female, pre-wired 12 AWG | loose nuts. Body 18.75 × 11.67, flange 34.25 × 15.85, ears 27.25 apart | same |
| J2, J5 | 2 | **4 mm binding post, red** | thread 7.45, 19 long | uxcell 10-pack (5 colours), [B08LN5T9D7](https://www.amazon.com/dp/B08LN5T9D7) |
| J7, J8, J6 | 3 | **4 mm binding post, black** | same pack | same |

## Joins and terminations

| Ref | Qty | Part | Notes |
|---|---|---|---|
| W1, W2 | 2 | **WAGO 221-415** five-port lever nut | ground bus; switched + bus |
| W3, W4 | 2 | **WAGO 221-413** three-port lever nut | input + join; input − join |
| — | ~1 m each | **14 AWG silicone wire**, red and black | every internal run |
| — | 3 | **6.3 mm insulated female spade**, blue (16–14 AWG) | the rocker's three tabs |
| — | 4 | **ferrules** for 14 AWG | the meter's four screw terminals. WAGOs take bare stranded wire |
| — | 6 | **ring terminals** for an 8 mm stud, 14 AWG | one per post, plus one for the LED return on J8 |
| — | 6 | **M2.5 bolts** | 2 per XT60E. Male: from inside, into its captive nuts. Female: from outside, nut inside |
| — | 4 | **M2.5 nuts** | for J3 and J4 |
| — | — | heat-shrink, 2–4 zip ties | zip ties hold the WAGOs to the base so they don't rattle |

## Leads

Built by you, from stock cables. See *Leads* in [WIRING.md](WIRING.md).

| Qty | Part | For | Source |
|---|---|---|---|
| 3 | **8-pin → 2× 8(6+2) PCIe splitter**, 18 AWG, 22 cm | one for the dual lead, two for the quad lead | Amangny 6-pack, [B094QSRK98](https://www.amazon.com/dp/B094QSRK98) |
| 2 (+1) | **AMASS XT60H male**, with sheath housing | the box end of each lead | Amazon, 5 pairs |
| 1 | **AMASS XT60H female**, with sheath housing | the box end of the bench-supply lead | same pairs |
| 1 short | **12 AWG XT60 pigtail** | the quad lead's splice point | |
| 1 | **4×8-pin → 12VHPWR adapter** | cards with the 16-pin connector | [B0GYHKK5WS](https://www.amazon.com/dp/B0GYHKK5WS) |
| 1 | **PCIe 1x→16x riser kit** (x16 board, x1 card, USB 3.0 lead, SATA → 6-pin) | docks on the deck | Kingwin, [B07QBF2X6C](https://www.amazon.com/dp/B07QBF2X6C) |

## The box

Printed from [`pcie-rig-enclosure`](https://github.com/IamMrCupp/3d-printer-models/tree/main/pcie-rig-enclosure) in 3d-printer-models. PETG throughout, about 300 g including the coupons.

| Qty | Part | Notes |
|---|---|---|
| 1 | `rig_base` | 142 cm³, feet down |
| 1 | `rig_cup` | 139 cm³, emitted deck-down |
| 2 | `rig_dock_rail` | pegs for the riser's mounting holes |
| 1 | `rig_cup_inlay` | optional second colour for the labels |
| 1 each | `deck_coupon`, `meter_fuse_coupon`, `xt60_coupon`, `joint_coupon`, `dock_rail_ladder` | print-first fit checks — see that README's print order |
| 4 | **M3 × 10** screws | cup to base, self-tapping into printed pilots |
| — | CA glue | the two dock rails |

## Bench

| Qty | Part | Notes |
|---|---|---|
| 1 | **current-limited bench supply**, 12 V, ≥ 6 A | mine is an OWON SPM8104. Set 12.0 V, OVP 12.6 V, 6 A limit. Never an ATX or server supply |
| 1 | DMM with continuity | every check in [BUILD.md](BUILD.md) uses it |

## Tools

Crimper for ferrules and spades, wire stripper, 2 mm hex or #1 Phillips for M2.5, driver for M3, calipers if you change anything.
