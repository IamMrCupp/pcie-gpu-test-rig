# Build sheet

Start to finish, in order. Parts and quantities are in [BOM.md](BOM.md); the wire-by-wire list and the two traps that fail silently are in [WIRING.md](WIRING.md). Read all three once before you cut anything.

## 1. Print the box

From [`pcie-rig-enclosure`](https://github.com/IamMrCupp/3d-printer-models/tree/main/pcie-rig-enclosure). That README has the print order and the print settings; the short version:

1. **Coupons first.** `deck_coupon`, `meter_fuse_coupon`, `xt60_coupon`, `joint_coupon`, `dock_rail_ladder` — about 70 g together. Push every panel part into its ladder, bolt an XT60 to each of its cutouts, drop the cup corner over the base corner and run an M3 in. Anything that doesn't fit changes a constant in `rig_common.scad` before the big parts print.
2. **Base**, feet down, no supports.
3. **Cup**, as emitted (deck on the bed), no supports. Add `rig_cup_inlay` as a second colour if you want filled labels.
4. **Two dock rails** at the peg size the ladder picked.

## 2. Fit the panel parts

Dry-fit everything in the bare cup before a single wire goes on. If something binds, fix the print, not the part.

1. **Meter** into the deck cutout from above until its spring clips catch.
2. **Rocker** into its hole from above until it snaps.
3. **Binding posts**: red into J2 (rear) and J5 (right), black into J7 (rear), J8 (right) and J6 (deck). Nut inside, then a ring terminal under a second nut.
4. **Fuse holder** through the rear wall, nut inside. Fuse out for now.
5. **XT60E-M** (J1): flange outside the rear wall, body through, M2.5 bolts from *inside* the box into the connector's captive nuts.
6. **XT60E-F** (J3 RISER, J4 CARD): flange outside the right wall, M2.5 bolts from outside, nuts inside.
7. **Dock rails** into their deck pockets with a drop of CA each. Check the riser board sits on them before the glue sets.

## 3. Wire it

Every join is a WAGO 221 lever nut: strip 11 mm, lift the lever, push the wire home, close the lever. Nothing is soldered and no terminal takes two wires. Follow the numbered rows in [WIRING.md](WIRING.md); the groups below are the order that keeps your hands out of your own way.

1. **Input** (rows 1–7). XT60 + pigtail and J2's ring terminal lead into **W3**; one wire from W3 through the fuse holder to the meter's terminal **3**. XT60 − pigtail and J7's lead into **W4**; one wire from W4 to the meter's terminal **2**. Ferrules into the meter.
2. **Meter to switch** (row 8). Terminal **4** to the rocker's **A** tab, spade.
3. **Outputs** (rows 9–12). Rocker **B** tab, spade, to **W2**. From W2 one lever each to the RISER + pigtail, the CARD + pigtail and J5. The fifth port stays empty.
4. **Ground bus** (rows 13–18). Meter terminal **1** into **W1**. From W1 one lever each to the RISER − pigtail, the CARD − pigtail, J8 and J6. The rocker's **yellow** tab goes to J8's terminal, with its own ring, under the same nut.
5. **Dress it.** Zip-tie W1 to the base floor and the other three to the bundle. Leave enough slack that the cup lifts 50 mm off the base without anything pulling.

Before you close it, beep the two traps:

- **Terminal 2 of the meter must not beep to terminal 1.** If it does, the input negative has found the ground bus and the meter will read 0 A forever.
- **The rocker's yellow tab must not beep to A or B**, rocker on or off.

## 4. Close it

Set the cup over the base so its skirt wraps the tongue, and run the four **M3 × 10** screws in from the sides. They self-tap into printed pilots; snug, not tight. Fuse in: **8 A fast-blow**, through the cap on the rear panel.

## 5. Make the leads

From [WIRING.md](WIRING.md) *Leads*: the dual lead from one splitter cable, the quad lead from two, each with a male XT60H on the box end. The bench-supply lead gets a female XT60H. Beep every lead end to end before it touches a card.

## 6. Checks before first power

Nothing plugged into J1, J2 or J7.

| Check | Expect |
|---|---|
| J1 + and J2 to meter terminal 3 | beep, through the fuse |
| J1 − and J7 to meter terminal 2 | beep |
| Meter terminal 2 to terminal 1 | **open** |
| Meter terminal 4 to rocker A | beep |
| Rocker A to every output +, rocker on | beep |
| Rocker A to every output +, rocker off | open |
| Meter terminal 1 to every output −, J8 and J6 | beep |
| Any + to any − | open, rocker on and off |
| Rocker yellow to A or B | open |

Then the first power-up, in this order:

1. Bench supply to **12.0 V, OVP 12.6 V, current limit 0.5 A**. Nothing on the outputs.
2. Plug the supply lead into J1. The meter wakes and reads about 12 V, 0.00 A.
3. Rocker on. The dot lights; every output + reads 12 V to J6.
4. Rocker off. Outputs dead, meter still lit.
5. Raise the current limit to **6 A**. Now, and only now, a lead goes on.

## 7. Use it

Riser on the dock, card in the riser, dual lead from RISER to the riser's 6-pin and the card, or the quad lead to CARD for a 16-pin card. Supply on, meter reading 12 V, then the rocker. What the current tells you is in the [README](README.md).

## 8. Service

Four side screws out, cup lifts off with all its wiring intact, base stays latched to the grid. Fuses change from outside through the cap.
