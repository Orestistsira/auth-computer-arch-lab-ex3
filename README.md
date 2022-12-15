# auth-computer-arch-lab-ex3

**Lab 3**

*Tsirakis Orestis (9995)*

*Iliana Kogia (10090)*

---

**Part 1**

---

1.

Power dissipation in a circuit is dynamic or static. 

As static and dynamic power are additives, each needs to be considered independently. Static power, which is also defined as “leakage,” is consumed in the absence of any design activity. It is highly associated with the current flowing through the transistor in idle state determined by the transistor attributes. Dynamic power is associated with the activity in the design influenced by the volume of data that the design has to process in a given time unit by switching the transistors between on and off states.

If two different programms run on the same CPU individually, as there is no power gating applied, only the dynamic power will be affected. The program that results in a higher dynamic power consumption is the program with the most flip-flop state changes. If power gating is applied, when the program is running the operating temperatute rises and increases the leakage power loss, so the static power can be affected depending on the usage of the processor.

Because McPAT generates consumption numbers that refer to power and not power consumption per hour, time duration does not matter.

2.

Energy efficiency is given by the formula: ef = (idle consumption * idle time) + (work consumption * work time). So there is a chance that the second processor is more energy efficient, as we dont know the work and idle times. McPAT can't give us a clear view of energy efficiency as these time parameters are not given in the results. We can get access to these parameters by a gem5 simulation.

3.

Xeon -> 50 times faster than A9

Xeon: Processor.Peak Power = 134.938 W

A9: Processor.Peak Power = 1.74189 W

Let's say the program on Xeon runs in 1 hour, so the Xeon CPU consumes 140x1=140Wh on full work state. From the assignment we get that the program on A9 will be 50 times slower and it will run in 50 hours, so the A9 CPU consumes 1.7*50=85Wh on full work state. So, even if the CPU goes off after finishing the program, it's clear that the A9 is more energy efficient than the Xeon as it consumes less Wh to complete the execution. If the CPU stays on idle after the execution, the Xeon processor will consume even more energy due to static power (leakage). In conclusion, the A9 processor is more energy efficient than the Xeon, even though the later is much faster on executing the program.

---

**Part 2**

---

1.

**EDAP = Energy x Delay x Area**, Where:

Energy: Total energy = Core.Subthreshold Leakage + Core.Gate Leakage + Core.Runtime Dynamic + L2.Subthreshold Leakage + L2.Gate Leakage + L2.Runtime Dynamic.

Delay: Total delay = the execution time of the program

Area: Total area = Core.Area + L2.Area

Set parameters from lab 2:

| Set Parameter | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| L1\_d | 32kB | 16kB | 16kB | 32kB | 32kB | 16kB | 32kB | 32kB | 32kB | 32kB |
| L1\_i | 32kB | 64kB | 16kB | 32kB | 32kB | 64kB | 32kB | 32kB | 32kB | 32kB |
| L2 | 512kB | 512kB | 512kB | 256kB | 2MB | 256kB | 512kB | 512kB | 512kB | 512kB |
| L1\_i\_assoc | 2 | 2 | 2 | 2 | 2 | 2 | 1 | 2 | 1 | 2 |
| L1\_d\_assoc | 2 | 2 | 2 | 2 | 2 | 2 | 1 | 2 | 1 | 2 |
| L2\_assoc | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 4 | 4 | 2 |
| Cache line | 64 | 64 | 64 | 64 | 64 | 64 | 64 | 64 | 64 | 128 |

Energy consumption values using the EDAP function:

| Set Parameters | bzip        | libm        | mcf         | sjeng       | spechmmer   |
| - | ----------- | ----------- | ----------- | ----------- | ----------- |
| 1 | 0.912259478 | 1.37091381  | 0.71394401  | 3.562322796 | 0.664368813 |
| 2 | 1.869847378 | 2.793176075 | 1.317596356 | 7.325485994 | 1.321694329 |
| 3 | 0.897093749 | 1.320001973 | 0.760758271 | 3.431419223 | 0.641161194 |
| 4 | 0.858430159 | 1.256899422 | 0.655100343 | 3.264414131 | 0.6097836   |
| 5 | 1.664559376 | 2.547374253 | 1.328206295 | 6.639469637 | 1.228675494 |
| 6 | 1.803736749 | 2.61567844  | 1.239022689 | 6.872454634 | 1.241245806 |
| 7 | 0.913162786 | 1.358605347 | 0.729704788 | 3.522758619 | 0.73672037  |
| 8 | 0.911474351 | 1.370731924 | 0.713622022 | 3.561956853 | 0.664246242 |
| 9 | 0.912311967 | 1.358270503 | 0.729373947 | 3.522381859 | 0.736590532 |
| 10 | 6.346390801 | 7.153359185 | 5.059286083 | 17.37271256 | 4.47767789  |

2.

**{1, 2, 3}**

<img src="./images/Picture1.jpg" width="800" height="480">

Observations:

Set parameter 1 and 3 give us the lowest peak power, and for set 1 we also get the optimum CPI from lab 2.

So we think that set 1 { L1_D=32kB, L1_I=32kB } would be the best choice.


**{1, 4, 5, 6}**

<img src="./images/Picture2.jpg" width="800" height="480">

Set 1, 4 and 5 are close to the lowest peak power, and for set 5 we also get the optimum CPI for the most benchmarks from lab 2. 

So we think that set 5 { L2=2MB } would be the best choice.

**{7, 8, 9}**

<img src="./images/Picture3.jpg" width="800" height="480">

Set 7 and 9 give us the lowest peak power, but set 8 gives us by far the best CPI for all the benchmarks.

As the peak power of set 8 is not that higher we think that set 8 { L1_D_Ass=2 L1_I_Ass=2 L2_Ass=4 } is the best choice.

**{1, 10}**

<img src="./images/Picture4.jpg" width="800" height="480">

Set 1 gives as by far the lowest peak power, although set 10 is better for CPI.

From lab 2 we got that Cache_Line_Size = 128 would increase the cost and as we see know it is not all energy efficient

So we think that set1 { Cache_Line_Size = 64 } would be the best choice.

3.

As we have know reviewed our architectures taking into account performance, cost and energy efficiency, we have all the tools to decide on an ideal architecture.

---

---

**Max Performance from lab 2:**

L1_Data = 32kB

L1_Instruction = 32kB

L2 = 256MB

L1_D_Ass = 2

L1_I_Ass = 2

L2_Ass = 4

Cache_line_size = 128

---

---

**Max Performance from energy efficiency:**

L1_Data = 32kB

L1_Instruction = 32kB

L2 = 2MB

L1_D_Ass = 2

L1_I_Ass = 2

L2_Ass = 4

Cache_line_size = 64

---

