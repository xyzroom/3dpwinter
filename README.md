# P-Winter V1

## Welcome
- P-Winter is (was) a CoreXY 3D printer based on the Hypercube and its successors.
- The aim was to create a 3D printer using only common and cheap RepRap components.
- This repository shall not be detailed. The V1 design is not ideal and was designed mostly when I was 14 with zero experience.
- I am currently working on P-Winter V2 and some other designs. The V2 concept is mostly done in CAD and hopefully will completely fix some of the silly design flaws and misunderstandings in V1.
- V1 cost estimate: approx 50 GBP, currency converted, for non-printed parts in the final printer, not including prototyping waste. Parts are cheap if you look in the right places ;)

# V1 Information and V2 Changes
## Overview
- There were a few fatal flaws with V1, as well as massive inconveniences.
- V2 strives to fix most of these. It aims primarily for: a more sensible belt path, a more sensible build volume, a filtered enclosure.

## Dimensions and V2 Enclosure
- V1 Frame (2020 T-slot extrusions): 380mm x 340mm x 500mm
- V1 Build volume: approx 210mm x 199mm x 270mm
- V2 will use the same frame with added extrusions for the enclosure and other attachments (e.g. filters).
##
- The V1 frame was not enclosable due to the Y endstop and part of the gantry spilling outside the frame volume.
- V2 changes this, compacting the design while offering a larger build volume. The current build footprint in CAD is a comfortable 220mm x 220mm. ('comfortable' means 1mm of theoretical space on either side of the extreme positions) With a minimal and empty toolhead carriage, the maximum travel can be pushed to a comfortable 250mm x 235mm.
- The Z axis is being shortened to ensure stability and enable the toolhead's Bowden tube and wiring to be enclosed comfortably.
- Previously the electronics for V1 where pulled outside an external enclosure to keep them cool. For V2, the electronics will be hidden at the bottom of the printer, separated from the heated chamber via an air gap.
- There will be fans underneath the heated bed to spread hot air through the enclosure.
- There will be a recirculating air filter at the back top of the enclosure and an exit air filter at the back bottom of the enclosure to maintain negative pressure.

## CoreXY
- V1 uses 8mm linear rods: 2x 300mm for Y and 2x 350mm for X.
- These are retained for V2. V2 will use LM8LUUs for Y and LM8UUs/LM8LUUs for X.
\ \
- V1 used 16T GT2 pulleys and idlers and 6mm steel-core GT2 belts, with 38mm NEMA 17 stepper motors.
- V2 keeps the motors but uses new belts and idlers:
  - The knockoff pulleys and idlers had questionable bearing quality/centred-ness/profile accuracy. I had spaced them incorrectly in the previous belt path.
  - The steel-core belts had questionable thickness and were incompatible with the small bend radius of the 16T pulleys and idlers.
- V2 will use proper belts and use stacked F695 flanged bearings as idlers. These have larger bearings designed for motion and are more likely to be round and centred.
\ \
- On top of the misaligned belt path in V1, my idlers were not operating smoothly on the threaded bolts I was using to hold them.
- V2 will use dowel pins or shoulder bolts to hold the idlers properly.
\ \
- V1 used a Hypercube-based belt path where the AB motors occupied space at the front of the Y axis. The motors were an eyesore and limited the travel in Y.
- The belt path has been completely redrawn for V2. It is now correctly aligned and parallel, and I have brought it as close to the enclosed extremities as possible, increasing travel in both X and Y. The AB motors have been moved to the back of the frame.
- The AB motors no longer need to be aligned with the belt path. The diameter of the pulleys no longer matter either. Either 16T or 20T can be used with minimal modification.
\ \
- Some magic with the belt path leaves 307mm of available rod length in the X axis. This allows for an 85mm-wide X carriage to travel 220mm comfortably in the X direction.
- The motors being in the back of the frame increases the available rod length to 267mm (up to 282mm). A 45mm-wide Y carriage can confortably travel 220mm (up to 235mm) in the Y direction.
\ \
- In V1, the motor mounts began to deform due to belt tension and motor weight acting together. The V2 motor positioning allows for a stronger, thicker mount with better-placed bolting holes. The belt tension now acts against the weight of the motor.

## Z axis
- V1 used a dual-Z setup with two 8mm x 350mm linear rods and a 350mm leadscrew on each side of the frame. (The 350mm leadscrew is too long for 350mm linear rods when using regular leadscrew nuts but this is not a major issue). This offered approximately 270mm in vertical travel
- V2 will use a similar dual-Z setup with 4 rods and 2 leadscrews, but shorten the Z axis to enclosure the printer better.
- For some reason I only had a 250mm heated bed. V2 replaces the 250mm bed with 210mm-spaced holes with a 220mm bed with 209mm-spaced holes.
\ \
- Both V1 and V2 do not have automatic bed levelling and utilise two motors driven by the same control.
- The original V1 -> V2 plan was to implement automatic bed levelling with three independent leadscrews. I decided against this because I would prefer to allocate these resources (added drivers, motors and axes) to my 250mm and 300mm printer projects.
- A 220mm printer really should just be properly trammed...
\ \
- The V1 setup used separate Z carriages (one extrusion) on each size of the printer, connected only via the heated bed and unreliable bed levelling springs. They were atrocious to tram relative to each other.
- V2 will use a mini frame made from 4 extrusions, such that the bed is bolted directly to the T-slot channels using silicon spacers. This will be far stiffer and easier to level.

## Toolhead
- V1 used a E3D V6 clone in a Bowden setup. V2 will most likely keep this.
- V1 did not end up with any part cooling. My newbie duct design had nil airflow and collided with the belts in the back, so I got rid of it and left it to V2.
- V2 will use radial blowers for part cooling.
- I am unlikely to switch to direct drive due to front/back space limitations as well as gantry stiffness concerns.

## Electronics
- The original setup was a classic 12V Mega/RAMPS/A4988 setup running Marlin 2.0. This was undeniably the cheapest possible setup and what I'm used to.
- Marlin took forever to compile. 3-axis hardware is not hard to build, but I'd like to get more involved with the software side of 3D printers. The new setup will run on Klipper and hopefully give me more control.
- The original heated bed could only reach 45 deg C on its own and 75 deg C in a box. The temperature raised slowly and raised Marlin time-out errors. I will be switching the printer to 24V electronics with Pi + SKR Pico.
- I will most likely keep using endstops rather than implement sensorless homing.
- V2 will use thermistors with known values rather than mystery 100k thermistors.

## V1 Performance and Other V2 Improvements
- Prints suffered from a wobble/layer shifting in the Y direction, on average in the correct position. I suspect this was due to play in the X axis rods and hot end nozzle, misalignment in the belt path and improperly-tuned stepper drivers. In V2, rods and bearings will be clamped down on rather than clipped or press-fitted into place.
- V1 homing used Makerbot-style endstops that are triggered by adjustable bolts on the moving carriage. This precision adjustment was good for the Z axis but unnecessary for the X and Y axes. Switching to simpler triggers.
- In general V2 is a design made by a more experienced me. The parts are more functional and the CAD is more detailed, avoiding issues in V1 where the lack of detail meant that bolts were inaccessible or that things would collide with the belt path.

## V2 Predicted Issues
- The frame (380mm x 340mm) can be considered small for a 220mm x 220mm build volume using full-size components (2020 extrusions and NEMA17) and linear rods. As such, the toolhead design is rather limited and cannot extend very far backwards (but it can upwards). This means that there is an undesirable centre of mass imbalance on the X rods in the V2 design. For this reason I am avoiding direct drive for now.

# Tips for next time
- Check the continuity of endstop switches and the resistance of heaters/thermistors with a multimeter. It took forever to figure out why the linear voltage regulator on my Mega kept frying. There was a solder bridge short circuit on one of my endstops!!!
- Tune steppers properly.
