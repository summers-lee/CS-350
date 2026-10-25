# CS-350
# Smart Thermostat Prototype: Project Reflection
## Summary of the project and the problem it solved
SysTec develops analytics software for servers and wanted to enter the smart thermostat market. Before building a Wi-Fi connected product, the company needed a working prototype of the low-level thermostat functionality. I built it on a Raspberry Pi development board. It reads room temperature from an AHT20 sensor over I2C and uses three buttons: one cycles the system between off, heat, and cool, and two raise and lower the set point through GPIO interrupts. A red LED fades for heating and a blue LED fades for cooling. The LCD shows the date and time, current temperature, and set point, and the thermostat sends its data over the serial port (UART) to simulate reporting to SysTec's server. I also wrote a report comparing Raspberry Pi, Microchip, and NXP architectures for the production version, judged on peripheral support, Wi-Fi, and Flash and RAM, and recommended one with justification.

## What I did particularly well
I was persistent and methodical when hardware did not behave. Early in the course my USB-to-TTL cable was not detected, and the serial test showed no data. Instead of changing code at random, I tested one layer at a time: whether the Pi saw the device (`lsusb`, `dmesg`), then permissions, then wiring, then the code. I also modeled the control logic as a state machine (off, heating, cooling) and drew it in draw.io before finalizing the code, which made the behavior easier to reason about and verify. [Add one thing specific to your final thermostat, such as smooth LED fading, reliable button debouncing, or clean shutdown behavior.]

## Where I could improve
My biggest lesson was time management. Hardware work takes longer than the code suggests, because wiring, permissions, and device setup all need time, and on earlier assignments I left too little room for that. I want to build a schedule that reserves time for debugging and for the demo video. I also want to test sooner and in smaller pieces, confirming the sensor, LCD, LEDs, and buttons individually before combining them. 

## Tools and resources I am adding to my support network

- **Command-line diagnostics:** `lsusb`, `dmesg`, `i2cdetect`, `groups`, and `ls -l /dev/...` for finding out whether a problem is hardware, permissions, or code.
- **SSH and `scp`:** for working on the Pi from my Mac and copying files between them.
- **draw.io:** for state machine documentation, including the Mermaid import for a first draft.
- **Documentation and community forums:** Raspberry Pi and Ubuntu documentation, plus forums for the libraries and boards I used.
- **My instructor and classmates:** for questions I could not resolve alone.
- **AI assistance:** as a tool for troubleshooting and drafting, with me verifying everything against the hardware and the documentation.

## Transferable skills
- **Systematic debugging:** isolating the failing layer, reading the real error message, and finding the cause instead of guessing.
- **State machine design:** a pattern that applies to any device or program with distinct modes.
- **Hardware and software integration:** reading from sensors, driving outputs, and handling interrupts and serial communication, which carries into any embedded or IoT work.
- **Security awareness:** the encryption work showed how small details, such as binary-mode file handling and key management, decide whether a system is safe.
- **Technical communication:** documenting a design for a team and justifying an architecture choice against business requirements.

## How I made the project maintainable, readable, and adaptable
- **Readable:** I used descriptive names, in-line comments explaining why the code does something, and a consistent structure.
- **Maintainable:** the logic is organized as a state machine, with the pin numbers and other settings defined in one place so they can be changed without searching through the code. [Confirm this matches your code.]
- **Safe by design:** the code cleans up GPIO pins on every exit path, including exit, quit, and CTRL-C, so the hardware is left in a known state.
- **Adaptable:** because the thermostat logic is separate from the hardware details, it can move to a different board or add the Wi-Fi connection in the next phase without a rewrite. [Edit this to reflect how you structured it.]
- **Documented:** the state machine diagram and the architecture report explain the design and the reasons behind it for the next developer.
