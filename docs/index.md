---
layout: default
title: Home
---

# FPGA Maze Solver

A wall-following maze solver built on an FPGA using the left-hand rule,
with IR + Ultrasonic sensors, PWM motor control, and an FSM at its core.

Built as part of [your competition/course name] — the robot didn't fully
solve the maze (the wheels kept slipping on the smooth surface), but the
FSM took turns at the right places, and we learned a ton.

## What's documented here

- How we generated PWM signals for motor control
- Frequency dividers to run sensor loops at different rates
- Configuring IR and Ultrasonic sensors with the FPGA
- Encoder synchronisation to prevent metastability
- The FSM logic for wall detection and left-hand rule navigation
- What worked, what didn't, and what comes next (Tremaux's algorithm)