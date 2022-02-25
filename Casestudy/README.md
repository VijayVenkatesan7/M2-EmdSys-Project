# MINE SAFETY SYSTEM:

# BLOCK DIAGRAM:
![image](https://user-images.githubusercontent.com/98878142/155695360-e2ed7b56-994a-4e30-b90d-18365c5d5754.png)
                 

# INTRODUCTION
   Today safety of miners is a major challenge. Miner’s health and life is vulnerable to several
critical issues, which includes not only the working environment, but also the after effect of it.
Mining activities release harmful and toxic gases in turn exposing the associated workers into
the danger of survival. This puts a lot of pressure on the mining industry. To increase the
productivity and reduce the cost of mining along with consideration of the safety of workers,
an innovative approach is required.These gases cannot be detected easily by human senses.A real
time monitoring system using wireless sensor network, which includes multiple sensors, is
developed. This system monitors surrounding environmental parameters such as temperature,
humidity and multiple toxic gases. This system also provides an early warning, which will be
helpful to all miners present inside the mine to save their life before any casualty occurs. The
system uses Zigbee technology to establish wireless sensor network. It is wireless networking
standard IEEE 802.15.4, which is suitable for operation in harsh environment. 

# ZIGBEE INTERFACING MODULE:
  ZigBee (Xbee) USB Interfacing Board is used to interface Xbee wireless module with
computer systems. This Board is used to connect ZigBee modules to make communication
between PC to PC or laptop, PC to Mechanical Assembly or robot, PC to embedded and
microcontroller based Circuits.As ZigBee communicates through Serial Communication so 
other end of USB which is connected to a PC, treated as COM port for Serial Communication.
It is provided with indication LEDs for ease.

# ARDUINO UNO:
  The Arduino board is a specially designed circuit board for programming and prototyping with
Atmel microcontrollers. The microcontroller on the board is programmed using the Arduino
Programming Language (based on Wiring) and the Arduino development environment (based
on Processing). It is relatively cheap and plug straight to computer’s USB port or power it with
an AC-to-DC adapter or battery to get started. 

# XBEE PRO S2B:
  The Xbee Pro S2B module is a wireless sensor network, which operates within the Zigbee
protocol and support the unique need of low cost and low power. This module requires
minimum power and provide reliable delivery of data between devices. It operates at 2.4GHz
frequency band.
 
# HIGH LEVEL REQUIREMENT:
  HR-1 It supports both AT and API mode. Its baud ranges from 2400 bps to 115200 bps. On this
interfacing board, CP2102 IC is used for converting TTL logic to USB logic.
  
  HR-2 Arduino UNO can communicate with a computer or other Arduino or other microcontrollers.
It communicates via serial communication (UART TTL). This serial communication appears
as a virtual com port to software on the computer.

# LOW LEVEL REQUIREMENT:
  LR-1 Zigbee USB Interfacing module is connected to the Router circuit.
  
  LR-2 The output is given to the microcontroller to take decicions whether to turn on alarm or not.
  
  


