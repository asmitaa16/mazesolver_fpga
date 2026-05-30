# Working with various sensors:

The bot needs to detect walls and also maintain a safe distance from them. Furthermore for implementing a closed-loop-control-system, we need to know exactly how much our wheels have actually moved compared to what we commanded. 

So, we use the following sensors:
- Infra-red obstacle detection sensor
- Ultrasonic sensor for distance measurement
- Wheel encoders for measuring distance travelled


### Infra-red sensors:
We use 3 IR senors placed in a star-configuration to detect walls on 3 sides and store the data in an array in the order of left-mid-right. The sensor outputs digital logic that reads a LOW when there's a wall and HIGH when the path is free. The proximity to the wall for detection can be adjusted using a potentiometer.

This module outputs the wall positions and is one of the most important ones (and the simplest of the sensors too) since we'll later base our maze-solving logic based on the presence of walls.


```verilog
//Reading the data and storing it in an array for future use
always @( posedge clk) begin
		  is_wall[0] <= infra[0];
		  is_wall[1] <= infra[1];
		  is_wall[2] <= infra[2];
    end

```

### Reading encoders:
Things get a bit tougher here. Let's first understand what and why. 
An encoder sends the controller a certain number of pulses during the time we are meausring. We rotate the wheel by hand first and count the number of pulses generated for a single rotation and then we can easily calculate the rotation speed from the number of pulses we received and the time period of observation.

But the method is very much dependent on accurately measuring the pulses. So, how does one ensure none of them are missed? We use what is called an interrupt- a method where the controller stops all its ongoing functions when an encoder pulse is received, runs a special function at that time (which is called an Interrupt Service Routine) which let's say increments a counter that stores the current pulse value. Perfect!

Well, not really. The problem lies in understanding how a procedural block works in Verilog. Clock is an important parameter in a sequential logic circuit. The way outputs change depend on which clock configuration we choose to read the inputs and trigger changes in the output accordingly. The "always" block showm below does this at every positive edge or rising clock edge i.e. when the clock pulse changes from LOW to HIGH. Now, our interrupt signal is not synchronous with our clock. This is termed as clock-domain-crossing- when a signal is asynchronous with our clock and brings up a "meta-stable" state where the output is not a stable 1 or 0. If the pulse is received near about the time when the clock is changing as well, there's a fair chance we might not read it at all. 

OK. Lot's of jargon. How do we tackle it then? That's much simpler- just hold on to the encoder pulse for one more clock pulse to make sure it is read by your controller. So, we store it in a flip-flop (1 bit register). That solves the problem of receiving the pulse.

The next challenge is to actually implement an interrupt. How do we confirm a change has occured in the encoder reading and change our counter variable based on that? We need to use a 2nd flip-flop for that. The first flip-flop directly stores the data from the encoder while the 2nd one holds on to the previous value read from the encoder. In this way we can detect a change in readings and be sure that a pulse had indeed been generated. 

The example below does it by detecting falling edges in the encoder pulse. Play around with it and try writing conditions resembling the RISING & CHANGE parameters of the Arduino attachInterrupt() function!


```verilog

always @(posedge clk_50)begin
        ff1 <= m1_encoder_a;
        ff2 <= ff1;

        if (ff1 == 1 && ff2 == 0)begin
            m1_ticks <= m1_ticks + 1;
        end        
    end
```

The diagram shows a typical synchronisation circuitry.
![PWM Generator Module](assets/images/sync.png)

*Image credit: https://daffy1108.wordpress.com/2014/06/08/synchronizers-for-asynchronous-signals/*


A synthesised module reading data from both wheel encoders and gives the encoder ticks as output for use by other modules.
![PWM Generator Module](assets/images/encoder.png)
