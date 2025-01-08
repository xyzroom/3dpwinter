# 3dpwinter

## Welcome
- P-Winter is a CoreXY 3D printer based on the Hypercube and its successors.
- The aim was to create a 3D printer using only (what I consider to be) common and cheap RepRap components.
- This repository shall not be detailed. The design is not ideal and was designed mostly when I was fourteen years old with zero experience.
- Rather than refine this design further, I am applying what I have learned towards other designs and P-Winter V2.
- Cost estimate: approx 50 GBP for the printer, not including prototyping, currency converted. Parts are cheap if you look in the right places.

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
- 16-tooth pulleys/rollers have more convenient dimensions than 20-tooth pulleys/rollers.
- Linear rods are much cheaper than linear rails. Rods and leadscrews can be found easily at lengths 200mm, 250mm, 300mm, etc.
- Mega/RAMPS is cheap and works fine for normal print speeds, though people considered it outdated even 10 years ago. Maybe use older, less bloated versions Marlin 1.9.xx versions or Klipper.
- I have not settled on a good fan duct design, through there should be infinite designs out there fore E3D V6 toolheads.
- Makerbot-style endstops are common and have clear mounting holes and wiring. (Bolts are screwed directly into printed plastic in my designs.)
- All axes use long M3 bolts screwed into plastic to adjust the homing positions. This is necessary for the z axis, but not so much the x and y axes. It might be better to just add small plastic arms to the printed design.
- The x carriage has plenty of spare bolt holes on the front and back for changing toolheads/fans/etc mounting. This allows for future expansion upon the toolhead design.
- Wire management uses zip ties and the grooves of the 2020 extrusions. This can be neat, but I pull my wires outside a makeshift enclosure and have not implemented closed electronics.
- The printer is not enclosed on the frame and parts spill outside of the frame area mostly because of wiring and the y bearing clamps.
- Some STLs included may seem thick or clunky. I've added thickness where I have observed parts deflect due to belt tightness.

## Performance
- Prints suffer from wavy patterns along straight perimeters. My belt rollers are probably misaligned or shifting. In V2 I will reduce the clearances on the belt path and try to reduce slack on the M3 bolts holding the belt rollers.
- Retraction settings need to be tuned for the Bowden extruder.
- At anything above a very low acceleration, prints have slight wobble/layer shifting in the y direction, on average in the right place.
  - The gantry was not secure in many places leading to play in the nozzle and x axis.
  - I suspect the stepper drivers are not tuned properly and/or are skipping steps due to the heavy moving x axis.
  - I don't think it is the z axis as it only happens in one direction.
  - Running at low accelerations causes corners to receive too much heat.
  - The issue is less pronounced when rotating parts by 45 degrees on the build plate, as it is distributed in both the x and y directions.
- Warping is an issue. The heated bed can only reach about 45 deg in open air and 75 deg with foam insulation in a box. The temperature raises slowly and I have to do it by 5 degrees at a time to avoid Marlin errors. (Errors could be avoided but I am trying to avoid modifying the firmware too much while tuning.) 24V electronics may resolve this.
- The heater heats very slowly, but has no problems sustaining temperatures if kept in an enclosure.
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


