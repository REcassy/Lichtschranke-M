# Lichtschrankenadapter-M
Open sensor for use with any standard light barrier on a Mobile Cassy.

This repo is under active development, so schematic and pcb files may not match always. Use the current release for production: https://github.com/REcassy/Lichtschranke-M/releases/tag/v1.0

## Compatible barriers
The Mobile Cassy pulls J2 to 5V (barrier 1) and J3 to 3.7V (barrier 2). Your light barrier needs to pull that down to less than 2V to register an event. A photo-transistor is optimal for that. You barrier can make use of +5V / GND jacks to power the light source. You should try to use as little current as possible to not put a strain on the Mobile Cassy's batteries, but anything up to 100mA seems to be acceptable.

Use at your own risk - especially drawing power. There is no public information on current limiting or fuses inside the Mobile Cassy. Always prefer LED to incandescent bulbs.

## Testing
For testing I included an Arduino simulator code. For this you need to connect the I<sup>2</sup>C pins of your Arduino (e.g. on a Uno Pins the upper right ones) to the I<sup>2</sup>C pins of the Cassy Mini-DIN interface (SDA: 1 and SCK: 5) as well as pin 7 of the Arduino (change this, if this is no digital out on your Arduino) to Mini-DIN pin 2.

## Programming your ATtiny25
The included ino file is intended for use with the Arduino IDE and any Arduino as an ISP Programmer. You need to:
* load the ISP sketch from the Arduino IDE (File->Examples->11. ArduinoISP) onto your Arduino Uno
* install ATTinyCore (https://github.com/SpenceKonde/ATTinyCore) as a board manager into your Arduino IDE 
* connect the Arduino to the ATTiny according to this graphic:

![Untitled Sketch_Steckplatine](https://github.com/user-attachments/assets/d0ae1926-4e57-458a-b34f-290312cf2cf5)

* when using other ATTiny chips check the datasheet or the ATtinyCore [repo][attiny-boards]
* set Tools->Board to ATtinyCore-> "ATtiny25/45/85 (no bootloader)"
* set Tools->Chip to ATtiny25
* set Tools->Programmer to "Arduino as ISP"
* use Tools->Burn Bootloader to set the appropriate E-Fuses in your ATtiny (only necessary with a brand new ATtiny)
* use Sketch->Upload Using Programmer

There are of course countless other ways to program your ATtiny. You can find the .hex file in the ATtiny directory.

## Schematic and PCB
The schematic and PCB files were created with KiCAD.

Be aware that earlier photos on my blog show a switched J4/J5 label (GND and 5V) as well as an incorrectly polarized C2.

The PCB file ending in "-tube" is used with brass tubes (see BOM) as connectors the one ending in "-jack" with ready made 4mm jacks.

Below you can see both boards fully populated:

![grafik](https://github.com/user-attachments/assets/75bc6a3c-8947-44a0-88a2-3af4b0098218)


## BOM
You need the following (given in brackets are Reichelt ordering numbers for reference):


| Part Label  | Description | Form factor | Reichelt number |
| ------------- | ------------- | ------------- | ------------- |
| U1  |  ATiny25 | DIP-8 | ATTINY 25-20 PU |
| U2 | USBLC6 | SOT-23-6 |  USBLC6-2SC6 |
| C1, C3 | 50V 100nF ceramic cap | 1206 |  WAL 1206B104K500 |
| C2 | 50V 10µF electrolytic cap | RM2,5 |  SU-A 10U 50|
| R1, R2 | 0,25W 5K1 resistor | 0207 |  1/4W 5,1K |
| J1 | Mini-Din 6 connector | N/A | EB-DIOS M06 |
| J2-J5 | 4mm ID, 5mm OD brass tube | N/A | N/A |
| J2-J5 | 4mm laboratory jacks | N/A | SEP 2610 F48  |

choose either J2-J5 option and the appropriate PCB design.

## Gerber and drill files
The gerber and drill files were exported from KiCAD and are ready to be sent to any PCB manufacturer of your choice. The PCB design features no vias. Any standard double sided process will suffice.
Please choose the correct set of files for your desired jacks.

Below are the renderings for both variants:

![](https://github.com/REcassy/Lichtschranke-M/blob/main/Renderings/Jack-top.svg?raw=true)  ![](https://github.com/REcassy/Lichtschranke-M/blob/main/Renderings/Jack-bottom.svg?raw=true) ![](https://github.com/REcassy/Lichtschranke-M/blob/main/Renderings/Tube-top.svg?raw=true)  ![](https://github.com/REcassy/Lichtschranke-M/blob/main/Renderings/Tube-bottom.svg?raw=true)

## 3D-printed case
A 3D printable case is currently in development.


[attiny-boards]: https://github.com/SpenceKonde/ATTinyCore/blob/v2.0.0-devThis-is-the-head-submit-PRs-against-this/avr/extras/ATtiny_x5.md
