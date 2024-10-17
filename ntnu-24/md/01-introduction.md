# Hardware hacking
## ... as a forensic tool

<br/>

Kjell Harald Andersen and Kim Espen Nyhus <!-- .element: style="text-align: left; font-style: italic; "> --> 
<br/><br/>

KRIPOS / National Criminal Investigation Service\
National Cyber Crime Center (NC3)\
Digital forensics section <!-- .element: style="text-align: left;"> -->


October 2024 <!-- .element: style="text-align: left;"> -->

--
## Some acknowledgement
> We would like to thank NTNU Gjøvik and Arvind Sharma for this opportunity to talk to you today. <!-- .element: style="text-align: left;"> -->

> Even though this lecture was created by Kjell H Andersen and Kim Nyhus, it is the accumulated skill and knowledge of many people both in the Norwegian police, and in various agencies across the world that has made this possible. <!-- .element: style="text-align: left;"> -->

---
## About - Kjell Harald Andersen
- Kripos since 2009
- Masters degree in signal processing from NTNU
- Background in analog and digital chip design
- Currently working on invasive methods for attacking silicon devices

--
## About - Kim Espen Nyhus
- Kripos since 2020
- Bachelor degree in micro electronics from NTNU
- Background in electronics and digital chip design
- Currently working on non invasive attacks (SCA/FI)

--
## About - KRIPOS
- Law Enforcement agency for fighting organized and serious crime
- National centre of competence for norwegian police
- National laboratories for forensics science
- National point of contact for international police collaboration
- National centre of cybercrime

--
## About - NC3
> Prevent, detect and combat threats and crime in cyberspace.

--
## About - Digital forensics section
> Extract data and other evidence from electronic devices.

--
## About - International collaboration
<img src="assets/international.png" alt="Internastional collaboration" height="600" />

--
## About - EXFILES
> EXtract Forensic Information for LEAs from Encrypted Smartphones

- Financed by Horizon 2020. Project budget of EUR 7 million over 3 years
- Aim: Develop new forensic models and methods for accessing data by bypassing security features in modern mobile phones; Non-invasive, semi-invasive and full invasive attacks. (Side channel attacks (SCA), fault injection techniques, secure boot bypassing, blackbox functions, …)
- 3 private companies, 5 academics and 5 LE agencies
- Website: https://exfiles.eu (with downloadable results)
- Status: Completed in October 2023

-- 
## About - Overclock
> Operational Vanguard: using Encryption Research for Criminal LOCKdown

- Financed by EU Internal Security Fund – Police (EU-ISFP)
- Project budget of EUR 4 million over 3 years
- Aim: Combat encrypted communication platforms used in organized crime and give police investigators access to decrypted data
- 4 LE agencies
- Status: Completed in September 2024

--
## About - ForRES
> Forensic Reverse Engineering of Silicon chips

- Financed by EU Internal Security Fund – Police (EU-ISFP)
- Project budget of EUR 4 million over 2 years
- Aim: Perform fully invasive operations on leading-edge semiconductor devices​ develop necessary tools and methods to attack the hardware chain of trust​ and advance the capability of extracting user data from highly integrated devices​.
- 3 LE agencies and 1 research institute (CSIC)
- Website: https://forres.eu


---
## The goal of this lecture
- Hopefully you will get some real world insight into
    - Feasability study and planning
    - Equipment and lab setup
    - Knowledge and skills
    - Digital forensics and risk assesment

--
## Main topics
- Hardware hacking in general
- SCA/FI
- Chip hacking
- Some examples

--
## And some practicle stuff
- We assume you know most of the basic technical lingo.
- If you have any questions, please note them down and hold on to them. Every now and then, there will be a checkpoint where we will address them. You'll know when it's time

---
# Questions so far?
