# Fault injection case study

---
## Trezor One

<img src="assets/trezor-one.jpg" alt="drawing" height="400" align="left"/>

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
- The PIN and encrytion seed was stored in plain text in RAM
- This attack became obsolete in later firmware

---
## Reproducing the attack
- Lots of public work on this device
    - Does not necessarily work anymore
- In the law enforcement context there are issues
    - Need close to 100% success rate
    - Consistant over sample specimen
    - Must know variation over chip revision and production site

--
## Some words on sample variations
- Process variation on silicon processes is very large
    - Some paramters may vary as much as 40%
    - The design in made to work inside this envelope
- SCA/FI pushed the device outside its design parameters
    - The effect of process paramters becomes unpredictable

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
- Close control of paramters
- On a given sample
    - Tune the paramters without damaging the chip
    - Repeat the attack with same result each time after tuning

--
### Main takeaway
>High Confidence - High repeatability - Low risk

---


---
## Questions