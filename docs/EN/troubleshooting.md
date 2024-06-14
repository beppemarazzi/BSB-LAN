# Troubleshooting

BSB-LAN tries to make accessing your heating system as easy as possible, but there are always things that can go wrong. If you still have a problem after reading this document as well as the [FAQ](faq.md), please [open up a bug report](https://github.com/fredlcore/BSB-LAN/issues/new?assignees=&labels=&projects=&template=bug_report.md&title=%5BBUG%5D) on the project's GitHub page and make sure that you provide us with all the necessary log files and further required details, especially from the Serial Monitor (or *SerMo* in short). You can access the Serial Monitor by going to ***Tools/Serial Monitor*** in the Arduino IDE. Make sure you copy the messages right from the moment your microcontroller boots until the moment you encounter the problem. Please do not send screenshots, only plain text files.

---
## Compiling fails: "Sketch too big"
- Select the "Minimal SPIFFS (Large APPS with OTA)" partition scheme in the Arduino IDE under ***Tools/Partition Scheme***.

---
## No data even thought the red LED is on
- Make sure the adapter is connected to CL+/CL- and not to the third (G+) pin: G+ will drive the LED, but it's not a data line.
- With the adapter for the Olimex microcontrollers: Make sure that the BSB-LAN adapter board sits **exactly** in the center of the UEXT connector. It will still fit in, if it's shifted one pin left or right, but it won't work.
- Make sure the RX/TX pins are set/detected correctly.

---
## Cannot query any parameters / device family is 0
- Wrong bus type (BSB instead of LPB or vice versa).
- If the red LED is not on (and ideally slightly flickering), there is a problem with the wiring between the adapter and the heating system. The red LED will come one once the adapter is connected correctly, even if the BSB-LAN adapter isn't even connected to the microcontroller!

---
## No or unreliable network connection
- Try powering the microcontroller via USB from a laptop. We have had many cases where power supplies were unreliable despite having sufficient ratings.
- Look at the Serial Monitor log to check if the microcontroller could acquire an IP address. If not, then your network settings or physical connection may be faulty.

---
## No connection to hidden WiFi network possible
- Yes, that is a known restriction. The only way to do that is to set the BSSID specifically in `BSB_LAN_config.h`.

---
## Room temperature (or any other parameter) cannot be set
- Check BSB-LAN's settings and make sure that write access is enabled and set to *standard* or *complete*.

---
## Web-interface freezes when making new connection
- BSB-LAN is not a multi-tasking system. This means it can attend to one task at a time. So even if a URL command is aborted (by closing the browser window), BSB-LAN might not detect this and only start serving new requests once the previous one is finished.

---
## The Serial Monitor is not showing readable data
- Make sure the speed is set correctly to 115200 bps.
- Make sure the correct port is selected.