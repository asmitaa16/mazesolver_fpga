# Mazesolver bot implementation in FPGA

Read through the pages for a detailed and fun guide to model maze-solving algorithm on an FPGA. Built as part of the e-Yantra Robotics Competition, it integrates data from Infra-red and ultrasonic sensors and wheel encoders and follows the left hand rule to solve the maze! All the coding is done using Verilog HDL, simulated and synthesised using Intel Quartus and we have finally used an Altera-USB-Blaster to program our bot using JIC files.


### What's documented here

- How we generated PWM signals for motor control
- Frequency dividers to run sensor loops at different rates
- Configuring IR and Ultrasonic sensors with the FPGA
- Encoder synchronisation to prevent metastability
- The FSM logic for wall detection and left-hand rule navigation
- What worked, what didn't, and what to build on

### Image Gallery :


![BOT1](docs/assets/images/bot3.png)

*The initial build- we used laser cut acrylic sheets for the body*

![BOT2](docs/assets/images/bot2.png)

*The sensors and the e-yantra provided PCB mounted- The bot's ready for a run here!*

![Maze](docs/assets/images/maze.png)

*Us with the Maze- the walls have been made by sunboard sheets pasted on the maze's plan*