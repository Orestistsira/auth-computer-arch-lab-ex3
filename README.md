# auth-computer-arch-lab-ex3

Part 1

---

1.

Power dissipation in a circuit is dynamic or static. 

As static and dynamic power are additives, each needs to be considered independently. Static power, which is also defined as “leakage,” is consumed in the absence of any design activity. It is highly associated with the current flowing through the transistor in idle state determined by the transistor attributes. Dynamic power is associated with the activity in the design influenced by the volume of data that the design has to process in a given time unit by switching the transistors between on and off states.

Should two different programms run individually, only the dynamic power dissipation will be affected (no power gating is applied) and the one causing the most flip-flop state changes will result in higher dynamic power dissipation. Should power gating be applied, then leakage power could also be affected depending on which CPU parts will be used. Well, to be precise, since leakage power is also dependant on the operating temperature, when a program runs and increases the dynamic power dissipation, the operating temperature rises thus increasing the leakage power loss.

Because McPAT generates consumption numbers that refer to power and not power consumption per hour, time duration does not matter.
