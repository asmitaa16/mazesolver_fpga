---
layout: default
title: References and Further Improvements
nav_order: 4
---

# Improvements:
There are so many more possibilities. Try implementing other maze-solving algorithms and optimizing them. Our problem statement required us to focus more on exploration, but you may absolutely take up one to solve the maze in the shortest amount of time and continue making hardware changes to increase speed and efficiency! 

# Some resources:

- This amazing series on Micromouse from UCLA! Definitely worth a look-

<iframe width="560" height="315" src="https://www.youtube.com/embed/ktn3C7aXVR0?si=8vMLYhS-tuDM_hkI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- Had to include a Veritasium video!

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZMQbHMgK2rw?si=DJ0blQ-mKRQJskMa" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- Tremaux's algorithm

<iframe width="560" height="315" src="https://www.youtube.com/embed/RjWSlz-aEr8?si=Tw8LLIOnJSPmDTK3" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Study bits:

- Refer to this [site](https://chipverify.com/verilog/verilog-tutorial) for your verilog doubts. Personally I've never been disappointed searching up information from here and on a side-note, LLMs might not be the best tools to provide you with help when dealing with synthesisable HDL codes so wrack your brains and study like the gold-old-days

- Metastability is an important concept when you're designing your controller on a FPGA. [Here's an article that provides some good explanation](https://www.asic-world.com/tidbits/metastablity.html)

- Now if you're not much familiar with hardware yet, jumping on to an FPGA would be an insane learning curve! So, instead get yourself acquainted with simple microcontrollers like Arduino. [This website](https://dronebotworkshop.com/arduino-microcontroller/) provides great tutorials and is my personal favourite.

- Concepts of [interrupts](https://dronebotworkshop.com/interrupts/) and [closed-loop motor control](https://dronebotworkshop.com/rotary-encoders-arduino/) , implemented in Arduino environments.

- Try using the signal tap logic analyser from within the quartus software to read the data from your sensors in real-time. Program the bot using a SOF (SRAM Object file)file and configure the analyser with the clock and the signals you want to view. Note that this is temporary and code gets deleted on power off.  To run the bot for trial, powered by battery, flash it using a JIC (JTAG Indirect Configuration) and code stays after reboot. 



