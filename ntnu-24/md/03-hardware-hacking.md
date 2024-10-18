# Hardware hacking

--
> Any activity that manipulates electronic devices in unintended ways with the purpose of gaining access to data or changing its behaviour. <!-- .element: style="text-align: left;"> -->

---
## Just a brief overview
So that we all are on the same page....

--
## What is HW hacking?
- There is a large number of techniques, methods and activities that will fit under this definition. 
	- Some are quite common and accessible
	- Some requires very specialized equipment and expertice
	- More will probably be added in the future
- This is not a complete list, but most of the more popular techniques are mentioned

---
## Reading memory devices
- Through existing interfaces
- In circuit
- Chip-off
- On die

 _Back in the old days ...._

--
<img src="assets/solder1.png" alt="drawing" height="500" align="left"/>
<img src="assets/mobile1.png" alt="drawing" height ="500" align="left"/>

--
<img src="assets/data_recovery1.png" alt="drawing" height="500" align="left"/>
<img src="assets/data_recovery2.png" alt="drawing" height ="500" align="left"/>

--
<img src="assets/data_recovery3.png" alt="drawing" height="450" align="left"/>
<img src="assets/data_recovery4.png" alt="drawing" height ="450" align="left"/>

---
## Fuzzing interfaces
- Low level
	- UART
	- JTAG
	- Debug
- High(er) level
	- USB
	- Network

_Software engineers seems to like this_....

--
<img src="assets/bb-usb.png" alt="drawing" height="500" align="left"/>
<img src="assets/usb_hack.png" alt="drawing" height ="500" align="left "/>

---
## Side Channel / Fault injection
- Power glitching and probing
- EM glitching and probing

_All over YouTube right now_....

--
<img src="assets/em_probe.jpg" alt="drawing" height="800"/>


---
## More Side Channel / Fault injection
- Laser glitching
- Photon emission probing
- SEM voltage contrast probing

_Next level_....

---
## Invasive silicon attacks
- Chip reverse engineering
- ROM content extraction
- Invasive probing
- Chip edits

_Tools for grown-ups_....

--
<img src="assets/fib1.png" height="600" align="left"/>

<table border="0" cellspacing="0" cellpadding="0">
	<tr border="0" >
		<td><img src="assets/chip1.png"height="250"/></td>
		<td><img src="assets/chip2.png"height="250"/></td>
		<td><img src="assets/chip3.png"height="250"/></td>
	</tr>
	<tr border="0" >
		<td><img src="assets/chip4.png"height="250"/></td>
		<td><img src="assets/chip5.png"height="250"/></td>
		<td><img src="assets/chip6.png"height="250"/></td>
	</tr>
</table>

---
## Reverse engineering
- PCB layout / schematics
- Interface protocols
- integrated circuits
- FPGA bitfiles

--

<img src="assets/reverse-sw.png" alt="Software reversing" height="520" align="left"/>
<img src="assets/chip-delayer1.png" alt="Chip reversing" height="500" align="left"/>

---
# Questions