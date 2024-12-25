# 3dpwinter

## Welcome
- 3D P-Winter is a CoreXY 3D printer loosely based on the Hypercube and its successors.
- The aim was to create a 3D printer using only (what I consider to be) common and cheap RepRap components.
- This repository shall not be detailed. Feel free to take inspiration, if any exists to be found, from the design. However I do not recommend using this design directly.
- This printer was designed mostly when I was fourteen years old with zero experience. Some aspects, particularly the z axis, can better utilise the lengths of the frame and linear rods.
- I am no longer making major changes to this design, except for a few pending modifications. Rather than refine this design, I am applying what I have learnt towards designing a new printer and renovating an existing one.

## Dimensions
- Frame dimensions 380mm x 340mm x 500mm (not fully enclosed and does not include extruder/filament/electronics)
- Build volume: 200mm x 200mm x 250mm (approximate, nearest 50mm)

## Parts I consider standard
Frame:
- 2020 profile T-slot aluminium extrusions
- Brackets + M5 bolts/nuts only. No drilling or tapping
Axes:
- 8mm linear rods + LM8UU linear bearings
- NEMA 17 stepper motors ~40mm
- 6mm 2GT timing belts + 16 tooth pulleys/rollers (6 toothed, 2 smooth)
- 8mm leadscrew + round brass nut + flexible spiral coupling
Electronics
- 12V PSU + Arduino Mega clone + RAMPS clone + LCD + drivers
- Heated bed + screws/springs/nuts
- Makerbot-style endstops
- E3D V6 clone + 3010 fan (+ any extruder if Bowden)
- 3010/4010/5015 fans
- Zip ties + tape + wire wrap

## Specific details
- Theoretical axial ranges (ignoring toolhead): ~210mm x ~199mm x ~270mm
- Frame extrusions: 4x 340mm (x dir) and 4x 300mm (y dir) 4x four 500mm(z dir) using T-slot nuts + metal brackets
- Bed extrusions: 2x 220mm for heated bed with 210mm-spaced mounting holes
- Linear rods: ~350mm (x), up to 300mm (y), 350mm (z, up to ~40mm shorter leadscrew)
- Printed parts mount to extrusions via M5 9mm bolts and T-slot nuts
- Everything else uses M3 bolts held by nuts, screwed into printed plastic or secured by gravity
  - 12mm usually
  - 8mm for mounting stepper motors
  - 28mm and 40mm, usually without nut, for holding rollers and adjusting endstops

## Design comments
- 16-tooth pulleys/rollers to me have more convenient dimensions than 20-tooth pulleys/rollers.
- Linear rods are much cheaper than linear rails. Rods and leadscrews can be found easily at lengths 200mm, 250mm, 300mm, etc.
- Mega/RAMPS is cheap and works fine for normal print speeds, though people considered it outdated even 10 years ago. Maybe use older, less bloated versions Marlin 1.9.xx versions or Klipper with an external Linux device.
- I used Bowden because I couldn't settle on a direct drive setup. I also have not decided on an ideal fan duct design. There are infinite designs out there for E3D V6 direct-drive extruders using part cooling with 3010/4010/5015 fans, but I've neglected that since I am only printing in ABS for now.
- Makerbot-style endstops are easy to find and have clear mounting holes and wiring. (Bolts are screwed directly into printed plastic in my designs.)
- All axes use long M3 bolts screwed into plastic to adjust the homing positions. This is necessary for the z axis, but not so much the x and y axes. It might be better to just add small plastic arms to the printed design.
- The x carriage has plenty of spare bolt holes on the front and back for changing toolheads/fans/etc mounting.
- Wire management uses zip ties and the grooves of the 2020 extrusions. This can be neat, but I have not implemented closed electronics and pull my wires outside the enclosure.
- The printer is not enclosed and parts spill outside of the frame area mostly because of wiring and the y bearing clamps.
- Some STLs included may seem thick or clunky. I've added thickness where I have observed parts deflect due to belt tightness.

## Performance
- Prints suffer from wavy patterns along straight perimeters. My belt rollers are probably misaligned or shifting. I am reducing the (frankly massive) clearances on the roller mounts and will use tape to reduce slack on the M3 bolts that hold the rollers.
- Retraction settings need to be tuned for the Bowden extruder.
- At anything above a very low acceleration, prints have slight wobble/layer shifting in the y direction, on average in the right place.
  - I suspect the nozzle has a lot of play due to the poorly secured, vertically aligned linear bearings and rods.
  - I suspect the steppers are not well-adjusted (they get very hot) and/or are skipping steps due to the heavy moving x axis.
  - I don't think it is the z axis as it only happens in one direction.
  - I run at very low accelerations (400 mm/s/s) in order to minimise this. However this may be causing corners to receive too much heat.
  - The issue is less pronounced when rotating parts by 45 degrees on the build plate, as it is distributed not just in the y direction.
- Warping is an issue. The heated bed can only reach about 45 deg in open air and 75 deg with foam insulation in a box. The temperature raises slowly and I have to do it by 5 degrees at a time to avoid Marlin errors. (Errors could be avoided but I am trying to avoid modifying the firmware too much while tuning.) 24V electronics may resolve this.
- The heater heats very slowly, but has no problems sustaining a temperature if kept in an enclosure.
- I have not tested part cooling.

## Issues and potential improvements
- Replace 8-bit controller.
- z axis:
  - Use cantilevered design or tri-levelling instead of 4 linear rods and 2 steppers/leadscrews, which has a high chance of binding.
  - Note: the separate carriages on both sides are currently not connected in any way other than the heated bed.
- x axis:
  - Reduce weight and improve stability. Add fans and direct drive.
- y axis:
  - Mount the stationary linear rods with clamps?
  - Keep everything within the frame volume so an enclosure can be made directly on the frame.
- The rollers on the y carriage are spaced by 10.186mm which is approx 32/pi. I am rounding to 11mm in the next design for convenience and to slightly account for belt thickness.
- Belt tightness causes the XY motor mounts to bend, requiring the motors to be supported against the frame with a spacer. A previous x carriage design also flexed outwards.

# Tips for next time
- Don't neaten things too early.
- Design parts so that they are intuitive to assemble in order.
- Account better for the space that brackets and bolts take.
- Check the continuity of endstop switches and the resistance of heaters/thermistors with a multimeter. It took forever to figure out why the linear voltage regulator on my Mega kept frying. There was a solder bridge short circuit on one of my endstops!!!
- Tune steppers properly.
- Get proper thermistors with known type/Marlin number/values instead of mystery 100k thermistors.
