# AD2000-M interface to Wemos D1 mini

## Introduction
It all started with some easy home-automation with home-assistant and while fidging with that I realized how fun it was to create and order PCB's to make my DIY projects a bit nicer!

This project is to make a nice mqtt bridge between a AD2000-M RFID keypad _(and all the variants of it)_ using a wemos D1 mini. It also uses a mosfet to act as a 12V relay for any electric lock that you might want to use in the door.

## AD2000-M Keypad
<img src="https://www.image-tmart.com/prodimgs_v2/8/8602/5094/86025094/AD2000M-Security-RFID-Proximity-Entry-Door-Lock-Access-Control-System_800x800.jpg?1495509344" width="200" height="200" />
The AD2000-M keypad is a cheap RFID keypad that can be found on various sites as aliexpress, banggood etc. and you should find prices ranging around $10 for the keypad and a bunch of RFID tags.
### Wiring
This is where it starts to get interesting since the wiring options apparently can differ between the same models based on who made them. Yeah... the AD2000-M name is widely used on all kinds of RFID keypads. This is how the most common model looks tough:
<img src="https://i.imgur.com/xYjru7m.jpg" width="200" height="200" />
Connect power to 12V and GND, 
PUSH should be connected to a button on the inside of the door to release the lock when going out.
NC goes to the lock/relay that you are using
Bell is to any signal that you want to use indoors.

## Schematic
<img src="https://i.imgur.com/HWfGYz1.png" width="400" height="400" />
This uses a 12V input and has a built in voltage divider down to 5V to power the Wemos. Software is basically whatever you want, I'm using either ESP Easy or ESPHome since it's easy to manage with OTA updates.
**PUSH** is connected to **D3** and is used to release the lock by using automation or a rule in the ESP
**D0 & D1** is a wiegand interface, actually not tried it yet in production.
**BELL** is connected to **D4** can trigger anything you want, I have a TTS message in my Google Home when someone pushes it.
**D6 & D7** on the Wemos is connected to I2C interface to be able to use a GY-21P sensor or anything else using the same protocol.
**D8** is connected to the Mosfet and will either lock or unlock the lock.

## Components
1000uF 25V 105C radial ø10x20mm
UKZ1E101MPM 100uF 25V 85C ø10x16mm
100nF 50V X7R 2.54mm
78S05 TO-220 5V 2A
Cooling fan TO-220 19.5x13x13mm
IRLZ44NPBF TO-220 N-ch 55V 47A
1N4001 DO-41 50V 1A
LED red 5mm flat topp
3x 10k Ohm resistor
