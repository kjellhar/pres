# Chip hacking

--
> What do we mean by that?

--
### Any operation that manipulats the actual silicon
- Reverse engineering
- Extracting ROM or fuses
- Probing internal signals
- Altering function

--
> How do we do that?

--
### With great effort and expense
- Requires expensive equipment
- Requires a very unusual skillset
- Usually very time consuming

---
## Let's look at som examples

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

- Focused Ion Beam
- Often combined with a Scanning Electron Microscope
- Can both image and manipulate silicon
    - Uses accelerated, focused gallium
    - Removes material by sputtering
    - By adding gasses, you can etch or deposit materials
    - ~10nm resolutions

---
## Unlock an Atmega controller

--
> This does not show the entire reverse engineering process. Only the actual attack performed at the end.
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

--
> As part of the Trezor One effort, we pursued several possible solutions. This attack was developed for a while, but when the glitch attack turned out to be more stable and successful than we imagined, it was abandoned. The concept may be applicable for other cases. <!-- .element: style="text-align: left;"> -->

> This section is heavy on microelectronics. Don't worry too much about the details, the main purpose is to illustrate the effort that goes into this kind of attack.  <!-- .element: style="text-align: left;"> -->

--
## The idea behind this attack
- Trezor One monitors attempts at getting access
- If it detects any tampering, it will erase itself
- This attack attempts to prevent any write operation to flash
- This would hopefully enable infinite attempts at brute forcing pin

--
## Technical overview
- Based on STM32F205 microcontroller
- Standard controller without any out of the ordinary security features
- Firmware is open source
- Silicon:
    - 40nm process (I think)
    - 1 Alu top layer, 1 thick Cu layer, 5 Cu routing layers
    - Integrated Flash
    - Possibly MiM capacitors

--
## Stackup of STM32F205RG

<img src="assets/stm32f205_stackup.png" height="800"/>

--
## Prevent flash from writing and erasing
- Flash is easy to find
- It is fairly easy to reverse engineer
- The flash write and erase depends on high voltage that is internally generated
- It should be possible to disable writing and erasing without messing with the read capabilities
    - Find and disable enable signals
    - Find and destroy high voltage charge pump
    - Find and cut the high voltage rail
    
---
## Delayer
- Expose each layer of metal routing
    - Lapping / polishing
    - Plasma etching
    - Wet etching
- Image each layer
- Analyse the results

--
### Top layer
<img src="assets/f205_dl1.jpg" width="1000"/>

--
### Top - 1 layer
<img src="assets/f205_dl2.jpg" width="1000"/>

--
### Top -1 layer Flash marked
<img src="assets/f205_dl3.jpg" width="1000"/>

--
### Bottom layer
<img src="assets/f205_dl4.jpg" width="1000"/>

--
### Flash
<img src="assets/f205_dl5.jpg" width="1000"/>


---
## Short primer on NOR Flash
- NOR flash is arranged in a grid
    - Word lines in columns
    - Bit lines in rows
- Only on cell in a row may be read or written to at a given moment
- Read by setting WordLine=High
    - Charge in floating gate will determine if the transistor is open or closed

--
<img src="assets/nor1.jpg" width="1000"/>

--
<img src="assets/flash_cs.jpg" width="1000"/>

--
## NOR Flash: WRITE
<img src="assets/nor_write.png" height="500" align="left"/>


- Set Drain to High Voltage (HV)
- Set Source to 0V
- Set Gate to HV
- Hot carrier injection -> Electrons into floating gate

--
## NOR Flash: ERASE
<img src="assets/nor_read.png" height="500" align="left"/>

- Set Drain to High Voltage (HV)
- Set Source to floating
- Set Gate to 0V
- Fowler-Nordheim tunneling -> drive electrons out

--
## NOR Flash: How it really is
<img src="assets/nor_really.png" height="400" align="left"/>

- We need to add a few transistors
    - Switch Gate between HV, Logic High and 0V
    - Switch Source between floating and 0V
    - Switch Drain between HV and sense amplifier
    -  Page selection switch on the Drain (Bit lines)

---
## On the die: Gate and source switches
(Image on next slide)
- These switches are above the flash cells
- The gates (Word Lines) are routed up through poly
- The sources are connected through M1
- Not yet sure which switches does what.

--
## On the die: Gate and source switches
<img src="assets/gs_switches1.jpg" height="700" align="left"/>
<img src="assets/gs_switches2.jpg" height="700" align="right"/>

--
## On the die: Drain switches
<img src="assets/d_switches1.jpg" height="650" align="left"/>
<img src="assets/d_switches2.png" height="650" align="right"/>

--
## On the die: Charge pump
<img src="assets/ch_pump.jpg" height="600" align="left"/>

- Disconnect HV distribution net
- Find potential attacks to destroy charge pump
- Manipulate the enable signal to the CP
- We ended our effort here

--
<img src="assets/ch_pump.jpg" height="900"/>

--
## Summary of the STM32F205 attack
- The reverse engineering effort so far is backed by many images not included here.  
- We still miss images of a couple of layers, which are necessary to identify the switches and the HV distribution nets
- The Trezor attack may not be that relevant anymore, but the principle of turning off the charge pump still is

---
## Questions
