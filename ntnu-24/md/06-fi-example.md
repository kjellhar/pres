# Fault injection case study

---
## Trezor One

<img src="assets/trezor-one.jpg" alt="trezor one" height="400" align="left"/>

- Hardware crypto wallet
    - Open hardware
    - Open source software
    - Based on the STM32F205RG microcontroller
- An attack by Joe Grand a couple of years back
    - Quite risky
    - Only works on early FW versions

---
## The Joe Grand attack
- Based on power glitching during boot sequence
- Enables the debug interface
- The PIN and encryption seed was stored in plain text in RAM
- This attack became obsolete in later firmware
- https://www.theverge.com/2022/1/24/22898712/crypto-hardware-wallet-hacking-lost-bitcoin-ethereum-nft

---
## Reproducing the attack
- More public work on this device
    - Does not necessarily work anymore
    - Kraken is quite interesting (https://blog.kraken.com/product/security/kraken-identifies-critical-flaw-in-trezor-hardware-wallets)

--
- In the law enforcement context there are issues
    - Need close to 100% success rate
    - Consistent over sample specimen
    - Must know variation over chip revision and production site

--
## Some words on sample variations
- Process variation on silicon processes is very large
    - Some parameters may vary as much as 40%
    - The design is made to work inside this envelope
- SCA/FI pushed the device outside its design parameters
    - The effect of process parameters becomes unpredictable

--
## Some parameters we can't control
- Carrier mobility
- Logic speed
- Threshold voltage
- Resistivity
- Gate oxide thickness

--
## Some parameters we can control
- Ambient temperature
- Supply voltage

---
## Planning and risk mitigation
- Extract data with as small risk of damage as possible
- Map sample variation
- Close control of parameters
- On a given sample
    - Tune the parameters without damaging the chip
    - Repeat the attack with same result each time after tuning

--
### Main takeaway
> High Confidence - High repeatability - Low risk

--
## Goal

### Read out entire flash content

---
## STM32 Security
- Readout Protection Level (RDP)
- Stored in special flash cells
- 3 levels of security
    - RDP0: No security measures, debug port is open, all flash and ram available
    - RDP1: Debug enabled, ram enabled but no flash access
    - RDP2: Debug disabled, and flash is locked

--
### Trezor One has RDP2 enabled

---
## Building the attack
- Examine the data sheet and reference manual
    - Identify key events in the boot loader that may be glitched
    - Find the glitch injection point closest to the kernel
- Inject power to glitch instruction execution at these key moments

-- 
### The attack vector
- On STM32 powerup, integrated BootROM executes first
- BootROM is accessible through a serial port
- In the BootROM there are commands for updating firmware
- And for flash memory readout

--
> Put the chip in a state where the flash readout is enabled

--- 
## Connecting the power
- Kernel instruction glitching
    - We want to corrupt instruction execution
- Attack as close to kernel as possible
- The reference manual may be helpful

-- 
<img src="assets/power-scheme1.png" alt="Power scheme 1" height="580" align="left"/>

- Internal V-reg for the kernel (marked yellow)
- Glitching external voltage not good
    - Through the V-reg will "remove" the glitch
- Bypass V-reg and glitch kernel directly
- Preferrably disable V-reg

--
<img src="assets/power-scheme2.png" alt="Power scheme 2" height="580" align="left"/>

- Remove decoupling of V-reg output
- Disable internal V-reg
- Apply external voltage
- Apply glitch directly to kernel

---
## Making the hardware
- A custom PCB is made
- Increase signal integrity
    - Signal source close to target
    - Small loop area
- Increase stability
    - Soldered connections
    - Safer to store and handle
- Reduce mess

--
<img src="assets/power-switches1.png" alt="Power scheme 1" height="500" align="left"/>

- Analog switches on power supply
    - Using MAX4619
    - 3 in parallel to decrease on-resistance
- Shunt resistor to measure current
- Also measure reset pin
- Connection to UART

--
<img src="assets/pcb.png" alt="Power scheme 1" height="800" />

--
<img src="assets/complete-setup.png" alt="Power scheme 1" height="800" />

---
## Some words on signal integrity
SKAL TENKTE LITT TIL PÅ DENNE
- Short lines
    - 
    - Paracitic effects (L and C)
- 

---
## Getting access to the bootloader

<img src="assets/bootloader-flowchart1.png" alt="Power scheme 1" height="500" align="left"/>

- This flowchart hides some essential facts
- Boot pins are checked during System Init
- If Boot pins are set, and in RDP0 or RDP1 mode
    - UART is enabled
    - Chip will expect commands on UART
- Glitch the system into RDP1 during System Init
    - Course timing from Reset signal
    - Fine timing from power spike when bootloader starts
--
<img src="assets/bootloader-glitch.png" alt="Power scheme 1" height="900" />

--
<img src="assets/bootloader_script.png" alt="Power scheme 1" height="900" />

--
<img src="assets/glitch_graph1.png" alt="Power scheme 1" height="900" />

--
<img src="assets/glitch_graph2.png" alt="Power scheme 1" height="900" />

--- 
## Read Memory command
- After bootloader is enabled flash read command is available
- But the command check RDP bit again before returning any flash content
- Must perform a new glitch for each read command
- Each read command only returns 256 bytes of data
- Must do the same glitch for each 256 bytes block of data

--
<img src="assets/read-cmd-flowchart.png" alt="Read command flowchart" height="950"/>

--
## Glitching the Read Memory command
- This glitche is first times from the UART command
    - Not precise enough
    - UART is not synchronized to program execution
- Timing is refined by current pulse when the process starts
    - Much like the bootloader glitch
- Glitch push the chip into RDP0 for this single execution of the command

---
## Summary
- By controlling the timing precisely, the glitch is extremely repeatable
- Solid setup prevents problems with EMI and poor signal conditioning
- Fine tuning must be done for each sample
- Even ambient temperature changes will throw off the timing

---
## Questions