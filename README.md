
## MarlinBraille 2
This repository contain the source code for the BrailleRAP firmware version 2.

MarlinBraille is a specialized version of Marlin firmware (https://github.com/MarlinFirmware) licensed under [GPL license](/LICENSE). Thanks for their beautiful work.

you will find the associated BrailleRAP configuration [here] (https://github.com/braillerap/MarlinBraille2Configuration)


## BrailleRAP SG fork (MKS TinyBee, ESP3D WiFi)

This fork's `xl-sg` branches carry the configuration for the [Singapore BrailleRAP XL](https://saadcaffeine.github.io/BrailleRap-SG/): an **MKS TinyBee v1.0** (ESP32) with TMC2209 drivers, **ESP3D WiFi** and **SD-card printing**. The first stable version is tagged [`xl-sg-v1.0.0`](https://github.com/saadcaffeine/MarlinBraille2/releases/tag/xl-sg-v1.0.0). The main differences from upstream:

- ESP3D WiFi re-enabled, with the AsyncTCP / ESP Async WebServer versions pinned so it builds on `espressif32@2.1.0`
- SD-card support, so WiFi hosts can upload a job and start it with `M23` and `M24`
- Y steps/mm set to 43.5 (`87/2` was integer division) and the paper sensor polarity fixed
- "Paper not loaded" cancels the job instead of halting the board, and cancel parks X instead of homing Y
- A power-on self test (X/Y wiggle and two solenoid taps), skipped after software restarts

**Optional on-device interface:** [BrailleRapSGUI](https://github.com/saadcaffeine/BrailleRapSGUI) is a web page served from the embosser itself. Upload its `braille.html.gz` to the ESP3D flash, then open `http://192.168.0.1/braille.html` from any phone or laptop on the embosser's WiFi. You can type English Braille (UEB grade 1), preview it, print over WiFi with progress and status lights, cancel, or emergency-stop. Desktop tools like AccessBrailleRAP and DesktopBrailleRAP keep working over USB as before.

Build with `pio run -e mks_tinybee -t clean` before `pio run -e mks_tinybee -t upload`. ESP3DLib reads Marlin's configuration through a computed `#include`, so without a clean build it can silently keep old settings. The wiring and setup notes are in [BrailleRap-SG](https://github.com/saadcaffeine/BrailleRap-SG/tree/master/MarlinBraille2-TinyBee-XL).

### Supported Platforms

  Platform|MCU|Example Boards
  --------|---|-------
  [Arduino AVR](https://www.arduino.cc/)|ATMEGA 2560| MKS Gen 1.4, MKS Gen L 2.1 

### Work in progress
  Platform|MCU|Example Boards
  --------|---|-------
  [ESP32](https://github.com/espressif/arduino-esp32)|ESP32|MKS TinyBee 

  
## License

Marlin is published under the [GPL license](/LICENSE) because we believe in open development. The GPL comes with both rights and obligations. Whether you use Marlin firmware as the driver for your open or closed-source product, you must keep Marlin open, and you must provide your compatible Marlin source code to end users upon request. The most straightforward way to comply with the Marlin license is to make a fork of Marlin on Github, perform your modifications, and direct users to your modified fork.

While we can't prevent the use of this code in products (3D printers, CNC, etc.) that are closed source or crippled by a patent, we would prefer that you choose another firmware or, better yet, make your own.
