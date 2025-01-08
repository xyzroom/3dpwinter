## Record for future reference

As was always inevitable I am completely rehauling the printer design. I am setting out with the ambitions following  

- DONE: filament spool holder (some pieces of extrusion attached to frame)
- DONE: Basic enclosure made from stacked storage boxes
- DONE: ESP32 camera breadboard circuit to spy from the inside of the enclosure

- TODO: Replace the oversized bed with a 220 mm sized bed that should hopefully reach higher temperatures.
- TODO: Increase the printable area from approx 210 mm by 200 mm to just less than 220 mm by 220 mm.
- TODO: Reduce the clearances for the rollers and belt paths. Round the spacings between rollers from 32/pi to 11 mm.
- TODO: Replace the steel-core timing belts with more flexible belts considering the tight bending radii and new belt path.
- TODO: Add part cooling, automatic bed leveling and a second hot end.
- TODO: Enclose the printer on the frame itself, keeping electronics and preferably steppers outside.
- TODO: Move the XY motors to the back of the frame to improve aesthetics and improve Y axis travel.
- TODO: Implement 3 independent Z axes (2 linear rods + 1 leadscrew + stepper).
- TODO: Replace noisy A4988s with either DRV8825s with TL smoothing or TMC2209s.
- TODO: Add a second Mega/RAMPS board to handle the dual extrusion and triple Z axes. Install Klipper on a computer.

# Z axis
The current configuration uses 2 linear rods and 1 leadscrew on each side of the printer. Each leadscrew has a separate stepper (big no-no) and both steppers are driven by the same driver (small no-no). This setup is overconstrained and having two steppers that may fall out of sync on power on/off is dodgy.  
While I have not had any issues with the bed needing to be releveled, this setup remains exceedingly suspicious. Also, tramming has been a nightmare as the bed leveling bolts are hard to access and the Z-carriages are separate, each holding onto one side of the headed bed.  
The new Z axis, which has already been designed, will use 3 Z axes consisting of 2 linear rods and 1 independently driven leadscrew each. The 2 extrusions from V1 will be formed into a T-shape to act as the Z carriage. The heated bed will be bolted firmly to the Z carriage at 3 points rather than 4, and using silicon spacers rather than springs. The Z carriage will be connected detachably to the 3 Z axes by K800 balls/magnets.  
The new system will be driven by weaker 23mm NEMA 17 pancakes. The main concern is whether having 3 leadscrews will introduce artefacts.
