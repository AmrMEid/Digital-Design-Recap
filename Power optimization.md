Power consumption became more critical in modern designs. modern designs demand a more functions and this leads to more transistors in same area. Two problems appear in this point. 

**Junction temperature:** more transistors mean more power consumption and more heat, increasing the junction temperature degrades the performance of all system.
**Battery life:** which affects significantly on user experience.


## Power Types:
The power consumption comes from 3 main sources:

![Asset 1-100](https://user-images.githubusercontent.com/43087648/215611989-20a137ef-839c-4522-bd95-6c96d11663e0.jpg)

- **Switching power:** this due to charging and discharging of the output node capacitor when changing the output value.

- **Short circuit power:** this happens when PMOS and NMOS are both ON and current flows from VDD to GND. this happen when the input voltage in the midrange between 1 and 0. this is a real problem if the slew rate of input signal is very slow. 

- **Leakage power:** even if the output node is unchanged. still some current flows in the CMOS gates in the reversed junction. leakage power dominates in the new technologies. 

**Leakage power sources:**
- from drain to source in weak inversion region.
- tunneling of electrons on the gate.
- minority carrier drift in depletion region.


## Power Factors



There are different factors to control the power consumption:
![1674231098168](https://user-images.githubusercontent.com/43087648/215612354-ccc786d2-1418-49fa-91a6-13d1800d0953.png)

- **Switching rate:** it is the probability of switching from 0 to 1 or vice versa for the given node in every CLK cycle. This factor affects the active power.
![1674232085918](https://user-images.githubusercontent.com/43087648/215612417-2070293e-fedd-4548-bc67-0d4ccdf71473.png)
 
- **Capacitance:** capacitive load of the output node which is the sum of the load from the next gate and the connection load. 
- **Voltage:** higher voltage means more current flows from source to the GND.
- **Transition rate:** more time in the transition means more time when PMOS and NMOS both are ON and current flows in the short circuit path. 
- **Device characteristic:** higher Vth means more resistance which reduces the short circuit current and the leakage current.

## Power Reduction Methods
There are different methods to enhance the results of power consumption and these reduction methods could be implemented in the different phases of chip design from the system level definition by dividing the system to different power domains to the gate level optimization to reduce the power consumption of each transistor. Methods for power reduction: 

1. **Optimizing the data flow:** in modern accelerators the data flows is a famous methos to reduce the switching power and increasing the reuse of operands to avoid computational and memory accessing power.
2. **Dynamic frequency:** reduce the frequency of the cores when executing non-timing critical task.
3. **Power islands:** partition the design to power islands depends on the performance requirement of each partition. this can significantly reduce the power consumption of non-critical modules. This needs to level shifters to shift up or shift down the shared signals to pass the noise range to avoid the short circuit current flow. This also increase the difficulty of verification because every island needs its timing and power specifications. needs more IO pins and more complex power grid.   
![Asset 2-100](https://user-images.githubusercontent.com/43087648/215612483-5e3ef064-96a8-4247-8c65-57a46a09fce7.jpg)


4. **Using shifters instead of multiplier:** multipliers are built with XOR gates which is power hungry gates. therefore, using shifters in constant multiplications can save power.
5. **Operand isolation:** switching on adders' inputs can lead to unneeded intermediate results which increase the switching power consumption. the reason of that is not all bits reach to the adder circuit in same time. therefore, registering the inputs will decrease the switching power but be note this will increase the latency.  
![Asset 3-100](https://user-images.githubusercontent.com/43087648/215612568-37713560-0d45-490c-988c-3038efec3052.jpg)

6. **Clock gating:** even if input to D-FF not changing still the switching on CLK input for the FF will consume power in the internal circuit of the FF. the closer the CLK gating circuit to the CLK source the more power saving done. because the most of dynamic power is dissipated in the high drive strength buffers in the CLK tree and have the most toggling rate. CLK gating circuit adds more area and power consumption of the latch and the and gate therefore it must be used only when enable circuit is expected to be low must of time. 
![Asset 4-100](https://user-images.githubusercontent.com/43087648/215612624-ed656db1-fcb5-45df-9c31-b3b7083cfcbb.jpg)
![Asset 5-100](https://user-images.githubusercontent.com/43087648/215612677-6a3129b6-6784-49d6-b312-c1165f8b55e5.jpg)

7. **Reducing VDD:** reducing VDD is powerful method because voltage is dominated in power formula. but decreasing the VDD will degrade the performance because it increases the gate delays. then it should be not used in critical paths circuits. also decreasing the voltage source needs to decreasing Vth which increasing the leakage power. this method is only effective when large voltage headroom.
Power gating: the most effective method to reduce the leakage power is selective shutdown for the unneeded modules. 
![Asset 6-100](https://user-images.githubusercontent.com/43087648/215612725-b437bf90-1020-4921-893a-57f188c5cd17.jpg)

it requires isolation cells between different power domains to avoid floating inputs for the next modules when power domain is OFF. PEn signal should be generated from always on circuit.

Don't switch large numbers of circuits in same time to avoid the current rush which may cause glitches and some nodes will not operate with good voltage conditions. 

Sleep and wakeup times must be calculated, and these are overhead on the performance because before going to sleep the circuit sometimes needs to save some states before losing them when power OFF. There are different methods to save states. using NVM memory to state retention is better in area and STDBY leakage because NVM can be switched off without problems but have a large read and write delay therefore this method is worse in timing performance. the other method is by using shadow regs which is better in terms of timing and energy consumption but requires more area and dissipate more leakage current during sleep. 

it needs to sleep and wake-up in correct sequence therefore to power OFF sequence (Stop clock -> Apply isolation -> save state -> apply reset -> power OFF). power ON sequence (Power on ->de-assert reset -> restore the state -> disable the isolation -> enable the clk) . 

8. **Decrease memory supply:** when it is not used, RAMs can't be powered OFF because it is a volatile memory. therefore, to decrease the leakage power it is recommended to reduce the supply (low Volt -> low leakage -> large delay).    
9. **Switching input pins:** connect the high activity net with the lower power consumption input:
10. **Using buffers:** to increase the drive strength (reducing the short circuit time) instead of sizing up the gates.
11. **Different Vth:** using high Vth gates to reduce the leakage power in the non-critical paths to maintain the timing results.




**References:** 
 Principles of VLSI RTL Design 
The Art of Hardware Architecture 
