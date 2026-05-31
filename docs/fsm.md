---
layout: default
title: The main Module
nav_order: 3
---

# The FINAL boss!

After configuring all our sensors and generating PWM signals, it's the right time to finally start building on the main algorithm that is supposed to be solving the maze! The journey is gonna be amazing, we promise!

There are quite a lot of tried and tested methods to solve a maze. To name a few, we have simple wall-following algorithms, search-based algorithms like Depth-First Search and Breadth-First-Search, path-planning based ones like A* or Djikstra's and the ones we like the most- Flood fill and Tremaux's algorithm. 

But here's the catch, we used none of them (LOL). Lemme be frank, we were first awed by the flood fill algorithm and made the arrays and wrote up the logic for updating values in the arrays as the bot traversed the maze, but it was highly expensive computationally and competition deadline constraints left us with little time for spending long hours on optimisation.

*(it's highly encouraged to explore all these algorithms and choose the one that works for you. For references, we'll add the ones we studied them from)*

So the plan changed. Our target now was to write a simple yet efficient algorithm for our bot to solve the maze. We had another constraint up our sleeves- the competition rules required us not to take the shortest path but to build an algorithm that visits as many of the dead ends as possible (8 did we manage to visit out the 9) and complete the whole exploration in a limit of 200 steps. The method we chose to achieve that was a simple rule: we receive data from the IR sensors about the presence of walls, then we continue making left turns unless there's a wall on the left. After a bit of tweaking the code to explore more deadends we successfully solved the maze in 116 steps!


![PWM Generator Module](assets/images/result.png)

Take a look at the following flowchart that provides a map of all the input and output signals from our main controller module:

![PWM Generator Module](assets/images/flow1.png)

Our main output signals would be connected to a motor driver module that controls the speed and direction of our wheels as directed by the controller. We used the simple and diy-bestie L298n motor driver for running our wheels. Controlling direction is fairly simple. You just gotta put the appropiate output signals from the main module to the motor driver INx pins to set the direction of rotation of the motors. And, here's a simple logic-flow to control the speed of the motors with PWM signals:


```verilog
if (counter == 400)  //we use a pwm frequency of 125 KHz 
    begin
    counter_pwm <= counter_pwm+1;
    if (counter_pwm == 255)begin
        counter_pwm <= 0;
    end

    counter <= 0;
    //set values of ena and enb accordingly to control speed
    //we kept the resolution 8-bit for familiarity to Arduino's analogWrite() function
    if(counter_pwm <= ena_pwm)begin
        ena <= 1;
    end else begin
        ena <= 0;
    end
    if(counter_pwm <= enb_pwm)begin
        enb <= 1;
    end else begin
        enb <= 0;
    end
end
```

Let us now look at building up the the main Finite State Machine block that is responsible for the main decision making. Look at the following flowchart for understanding the decision-making rules. Just lemme give a little brief-up first: The first thing to look at is the sensor data telling us where the walls are. So we have a 3 input values to our module in the order left-mid-right. A value of "000" means we have successfully exited the maze and a value of "111" means we have hit a dead-end. Anything in between these values would require us to make decisions and take turns accordingly. The choice-making is simplest when the path is blocked on both sides and as per the plan we take left turns while the path to left and right/mid is open too. To keep track of the movements we also maintain a 2-bit variable that contains which side our bot is facing, mapped as "00" to North and rotates anticlockwise for the other directions.

A little hack here is to move the bot block-by-block since that worked best for us! You may play around with other possible approaches, for e.g. moving the bot as long as a wall is encountered. 


How do we make the turns? The wheels must rotate in different speeds to make the rotation possible. As for how to know when the turn has been completed, we count the encoder pulses till the start-to-end of the turn. You can obtain quite perfect 90 degree turns with some trial and error.
Here's an example left turn logic according to the values we had obtained:


```verilog
always @(posedge clk)begin
    if (ticks_m1_a <= 435 && ticks_m2_a <= 435) begin
        speed_l <= 130;
        speed_r <= 180;
    end
    
    else begin
        speed_l <= 0;
        speed_r <= 0;
        done <= 1;
    end
    
end
```
<!-- 
```verilog
```

```verilog
```

```verilog
``` -->



