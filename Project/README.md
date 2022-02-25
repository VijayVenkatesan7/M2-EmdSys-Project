# DRIVING LICENSE VERIFICATION
  
# INTRODUCTION:
     The finger-print based System for driving licensing verification. Biometrics is one of the most critical emerging technology. As the world becomes more volatile and potentially more vulnerable to fraudulent forces, our fate lies within our ability to secure and protect critical data and facilities. From these different available biometric features Finger Print is one of the best features which provides good mismatch ratio and reliability. Driving without license is a major issue in many countries. Survey says that the accidents happened mostly by unlicensed drivers. The new system Finger print identification is proposed.We represent the design of a prototype automatic license verification system and its implementation. It uses fingerprints to verify the identity of an individual. If the finger print stored in the controller and finger print swiped in the device matches, he/she can proceed for ignition and otherwise ignition will not work. This will reduce the accidents happened by unlicensed drivers.
     
# BLOCK DIAGRAM:
  ![WhatsApp Image 2022-02-25 at 8 06 23 PM](https://user-images.githubusercontent.com/98878142/155733653-e16e8ad9-de75-41d4-a894-eec8c7d4dca9.jpeg)
  
  The Microcontroller is surrounded by r303a finger print scanner , Step down transformer for power supply, Relay , LCD.The LCD is connected to the pic microcontroller to           displays the process.The microcontroller is a programming tool to run the entire operation.

# MICROCONTROLLER:
  Various microcontrollers offer different kinds of memories and the microcontroller we used is shown in the block diagram. EEPROM, EPROM, FLASH etc. are some of the memories of which FLASH is the most recently developed. Technology that is used in pic16F877A is flash technology, so that data is retained even when the power is switched off. Easy Programming and Erasing are other features of PIC 16F877A.
  
# RELAY:
  Relay is an electrically operated switch. Current flowing through the coil of the relay creates a magnetic field which attracts a lever and changes the switch contacts. The coil current can be on or off so relays have two switch positions and they are doublethrow (changeover) switches. Relays allow one circuit to switch a second circuit which can be completely separate from the first. For example a low voltage battery circuit can use a relay to switch a 230V AC mains circuit. There is no electrical connection inside the relay between the two circuits; the link is magnetic and mechanical. The coil of a relay passes a relatively large current, typically 30mA for a 12V relay, but it can be as much as 100mA for relays designed to operate from lower voltages. Most ICs (chips) cannot provide this current and a transistor is usually used to amplify the small IC current to the larger value required for the relay coil.
  
# STEP DOWN TRANSFORMER:
  The potential transformer will step down the power supply voltage (0-230V) to (0-15V and 0-9V) a level and block diagram . If the secondary has less turns in the coil then the primary, the secondary coil's voltage will decrease and the current or AMPS will increase or decreased depend upon the wire gauge. This is called a STEP-DOWN transformer. Then the secondary of the potential transformer will be connected to the rectifier.
  
# FINGERPRINT SENSOR:
  Fingerprint processing includes two parts: fingerprint enrollment and fingerprint matching which is used .When enrolling, user needs to enter the finger two times. The system will process the twotime finger images, generate a template of the finger based on processing results and store the template. When matching, user enters the finger through optical sensor andsystem will generate a template of the finger and compare it with templates of the finger library. For 1:1 matching, system will compare the live finger with specific template designated in the Module; for 1:N matching, or searching, system will search the whole finger library for the matching finger. In both circumstances, system will return the matching result, success or failure.
  
# LIMIT SWITCH:
 a limit switch is a switch operated by the motion of a machine part or the presence of an object. A limit switch can be used for controlling machinery as part of a control system, as a safety interlock, or as a counter enumerating objects passing a point.Limit switches are used in a variety of applications and environments because of their ruggedness, ease of installation, and reliability of operation. They can determine the presence, passing, positioning, and end of travel of an object. They were first used to define the limit of travel of an object, hence the name "limit switch".
 
# HIGH LEVEL REQUIREMENTS:
|  ID  |             Description                                 |
|:-----|:--------------------------------------------------------|
| HR-1 |  Processor read/write access to program memory          |
| HR-2 |  Wide operating voltage range: 2.5V to 5.5V.            |
| HR-3 | High Sink/Source Current:25 Ma and Low-power consumption|







     
     
