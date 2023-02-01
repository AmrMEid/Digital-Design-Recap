# Asynchronized Reset

## Asynchronized Reset advantages:

- Requires less area and power because it connect directly to FF pins.
- No need to CLK existence.

## Asynchronized Reset disadvantages:

- sensitive to glitches.
- can lead to metastability.

# Synchronized Reset

## Synchronized Reset advantages:

- Avoid reset glitches
- all circuit are synchronized on reset and operations. 

## Synchronized Reset disadvantages:

- Requires CLK existence.
- requires more area and power because it needs gates and muxs and not connected directly to the FF pins.
- rst assertion must be wide enough to meet the CLK edge. 


# Reset Domain Crossing(RDC)

metastability can be happened if 2 FF have different asynchronized reset then if the source FF rst signal is asserted in the window of metastability (setup  time+hold time) therefore the destination FF may go not stable state. 

RDC are hard to catche because it needs the system analysis and how resets signals are interacted with each other and reset sequence and resets are happened in lower rate than CDC.

RDC are global and can be propagated on gates, but CDC check is done only on the domain crossing interface. 



## Solutions: 

1. **RST synchronizer**: same as CDC solution we can use double FF solution to avoid metastability, then even if first FF goes to metastable state it will have enough time to reach stable state. 
2. **RST ordering**: de-assert RST1 first then RST2 or assert RST2 first then RST1
3. **CLK gating**: if FF2 has gated CLK then disable its CLK first then assert RST1 safely.
use reset check tools. 


# Reset Synchronizers

sometimes we need the best of both worlds when therefore we need that circuit be rested asynchronously and de-assert only synchronously. 
