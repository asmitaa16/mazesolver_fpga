# Mazesolver bot implementation in FPGA

Read through the pages for a detailed and fun guide to model maze-solving algorithm on an FPGA. Built as part of the e-Yantra Robotics Competition, it integrates data from Infra-red and ultrasonic sensors and wheel encoders and follows the left hand rule to solve the maze!


### What's documented here

- How we generated PWM signals for motor control
- Frequency dividers to run sensor loops at different rates
- Configuring IR and Ultrasonic sensors with the FPGA
- Encoder synchronisation to prevent metastability
- The FSM logic for wall detection and left-hand rule navigation
- What worked, what didn't, and what to build on