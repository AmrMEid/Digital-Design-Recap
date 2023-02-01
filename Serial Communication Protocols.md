Across last years, using serial communications protocol get a more reputation to solve the problem of sending many bits in parallel. Although using parallel communication may gain more performance as sending n-bits in same CLK cycle, but it fails when increasing the transmation speed for long distance. as examples:

Cost:  when sending parallel bits to another device you need many wires and more distance to cover means more wires and more cost.
CLK frequency: when distance is increasing, the skew between different bits in same packet will increase therefore the serial communication is better when sending data with high speed for long distances.  
Cross talk: when sending parallel bits in high speed the adjacent lines will affect on each other and some bits may be changed, and the data is damaged.


I2C Protocol 






Add alt text
No alt text provided for this image
It is a widely used synchronized serial communication protocol that is used in many applications.

It consists of two signals SCL(clock pin) and SDA(data pin). in IDEL state both lines are should stay HIGH then SCL and SDA should be connected by pull up resistors. 

Frame:

start conditions: SDA transition from HIGH to LOW while SCL is HIGH
Address phase: master sends 7bits (or 10 bits) of the slave address. Then 1 bit that indicate master needs read from or write to the slave device(WR=0 write and WR=1 read).
Data phase: Data is sent in bytes followed ACK bit (MSB frist).
Stop condition: SDA transition from LOW to HIGH while SCL is HIGH.


Any transition on SDA line (except start and stop bits) should be happened only while SCL is LOW. 
Each master should check the SDA and SCL is HIGH before sending the start bit to make sure no other master hold the bus.
CLK stretching can be done by hold SCL LOW for an extra time to process the received commands instead of sending NACK. any device on the medium can do CLK stretch   therefore debugging it is tricky in debugging and need to remove one device per time to find the device that hold SCL LOW/
Advantages of I2C protocol:

cheap and requires only 2 lines.
support multi masters and multi slaves communications.
each frame has its ACK confirm.
Disadvantage of I2C protocol:

Half duplex 
data frames are limited to 8 bits.
Slow compared to SPI (from 100 KHz to 5 MHz).


SPI Protocol 
It is a serial commination protocol that is used to connect different peripherals to such as flash memory. it consists of 4 lines. 







Add alt text
No alt text provided for this image
SCLK: clock line

CS: chip select, each salve should be connected to 1 CS pin.

MOSI: master out slave input.

MISO: master input slave output. 

When in IDLE state CS should be HIGH. and be LOW during the data transmission.

Steps:

generate the CLK.
hold CS LOW
Data transmission using MISO or MOSI and synchronized with SCLK line. Data is sent on MOSI line with MSB first and on MISO line LSB first. 
Clock polarity: choose data are out and sampled on positive edge of falling edge.

Clock phase: data output on first edge or second edge regardless it is rising or falling edge.

Advantages of SPI protocol:

No start bit or stop bit then data can be sent in stream. 
High data rate(up to 10 Mbps).
Full duplex
Disadvantage of SPI protocol:

Use 4 wires.
No ACK for successful transfare. 
No error checking such as UART parity bit.
Only Single master on the bus.
Daisy-chain Topology:







Add alt text
No alt text provided for this image
Master module should implement CS pin for every slave on the bus therefore it adds complexity on routing and connections. to connect all slaves on single master CS pin, daisy chain topology is used. 
 By connecting all slaves on same CLK and CS pins and connect every slave MISO pin to the next slave MOSI pin. every slave should support forwarding data from DIN to DOUT without delay. 
 Steps:

generate CLK
Hold CS LOW
send bits in sequence.
CS is HIGH then every slave should execute its command.




UART Protocol 
it is asynchronous communications protocol that used to data exchange with low data rate. 

The TX line from one device should be connected to the RX line of the other device.
The two devices should have same baud rate before communications start. 






Add alt text
No alt text provided for this image
Steps:

start bit: Hold TX line LOW.
Data: send from 5 to 8 bits with LSB first.
Parity: can be even or odd parity.
Stop bit: Hold TX line HIGH for 2 cycles.
Advantage of UART protocol:

requires only 2 lines.
No CLK signal.
parity bit for error checking. 
Full duplex.
Disadvantage of UART protocol:

packets limited to 8 bits.
only 1 master and 1 slave.
Baud rate offset must be less than 10%
Slow compared to SPI.
