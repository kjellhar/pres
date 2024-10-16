# Chip hacking

--
> What do we mean by that?

--
### Any operation that manipulats the actual silicon
- Reverse engineering
- Extracting ROM or fuses
- Probing internal signals
- Altering function

---
LITT MER GENERELT

---
## A Simple lock bit hack
- Most microcontrollers have code protection
- Older devices - Single fuse or EEPROM bit
- Flipping the bit -> Code is readable
- Some controllers used more bits

--
## The first lockbit hacks
- UV light attack
- Super simple and low cost
- Masking everything except the lock bit
- Easily countered by chip designers

--
## More advanced
- Partial reverse enginnering
- Find lock bits, and how they are programmed
- Edit the chip using a FIB

---
## What's a FIB?

--
## What's a FIB?
<img src="assets/fib2.jpg" height="600" align="left"/>

- Focussed Ion Beam
- Often combined with a Scanning Electron Microscope
- Can both image and manipulate silicon
    - Uses accelerated, focussed gallium
    - Removes material by sputtering
    - By adding gasses, you can etch or deposit materials
    - ~10nm resolutions

---
## Unlock an Atmega controller

--
<img src="assets/atmega1.png" height="900" />

--
<img src="assets/atmega2.png" height="900" />

--
<img src="assets/atmega3.png" height="900" />

--
<img src="assets/atmega4.jpg" height="900" />

--
<img src="assets/atmega5.jpg" height="900" />

--
<img src="assets/atmega6.png" height="900" />


---
## Reverse engineering a STM32F205



---
## Questions
