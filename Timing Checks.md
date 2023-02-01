
Development cycle of any design takes many years and every generation tend to operate on higher frequency but as we will see, the timing results of transistor gates are dependent on many factors and on the simulation vectors therefore we need another method to verify the chip will operate on target frequency without faults. Static timing analysis (STA) is the method that used to validate that signals reach all points in the desired time without generating all simulation vectors because it measures only the maximum and the minimum frequency that design can operate therefore it doesn't need any simulation vectors. but be careful that STA doesn't solve the logical errors.

**There are some definitions that we need to know before we go through the timing checks:**

- **Slew:** it is the time that takes to change the output voltage value from 0.1 VDD to 0.9 VDD.


Add alt text
No alt text provided for this image


- **Skew:** time between 0.5 VDD on input pin to 0.5 VDD on output pin. 


Add alt text
No alt text provided for this image


- **Uncertainty:**

1. Jitter: PLL variations in every CLK edge.

Add alt text
No alt text provided for this image


2. CLK source skew: not all CLK paths to every FF in the design have equal delays.

Add alt text
No alt text provided for this image
# Timing Parameters:
every gate is different from the other gates in timing results because it heavily dependent on various parameters. 

- **Geometry gate**: smaller technologies are faster (but have more leakage current).
- **Output pin load**: the sum of interconnect load & load of next gate driven.
- **Input slew**: depends on transition time of pervious output & interconnect capacitance & input delay & drive strength of the driver gate. 
- **Temperature**: more temperature will decrease the mobility of electrons then the gate delay will increase.
- **Voltage**: gates operate faster with high voltage. 
- **Process**: Gates with less Vth have small delay (but more leakage current).

# Timing Checks:
## Setup Check: 
it is the time before CLK edge that data should be stable to be captured correctly by the FF. if data is changed during this window , the FF output will go to an undefined state.


Add alt text
No alt text provided for this image
Setup check is done with the worst conditions on data paths and best conditions on CLK paths.


Add alt text
No alt text provided for this image


Setup violations are solved by pipelining (to decrease the combinational path delay) or operate on lower CLK frequency.

## Hold Check: 
it is the time after CLK edge data should be stable to avoid the propagation of the new data and missing capture of the old data. If gates are so fast, then the new data will be captured with the FF. 

Add alt text
No alt text provided for this image


Hold check is done with the best conditions on data paths and worst conditions on CLK paths.


Add alt text
No alt text provided for this image


Hold violations are solved by increasing the combinational delay or by operating on less Voltage. 


Add alt text
No alt text provided for this image

# Timing checks on Reset signal:
reset signal is heavy loaded signal and very important as it helps the design to go to a defined IDLE state therefore, we need timing checks to ensure all design will go to stable state without glitches. 

**Recovery Check**: time after RST signal de-assertion & CLK shouldn't be come to see CLK effect.

**Removal Check**: time after CLK edge that RST signal should stay asserted to avoid the CLK edge effect.
