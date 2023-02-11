This instruction should be used to waste a standard instruction cycle length. This could be used to create real time delays without putting extra load on the processor. This instruction will not interact with storage units, memory, registers, or any other resources of such that store data. This instruction will continue as a normal operation. Operations executed after this should be expected to run normally, no influence will be created by this.

# Usage as Delay
```asm
[Static]:
int iterations = 0;

[Executable]:
Main:
	JumpIfXOR(iterations, 99998, &AfterFinish);
	Add(iterations, 1);
	NoOperation(); // 99998 (NoOperation) + 1 ( JumpIfXOR ) + 1 (Add) = 100000
	
AfterFinish:
	Kill();
```

This program will cost `100000` instructions in the main routine. If the clock speed is `1000 Hz` then the programs time can be determined from the following, `(1000 [milleseconds] / 1000 [Hertz]) * 100000 [Instruction calls due to delay/main function] + 1 [int iterations] + 1 [Kill] = 100.002 [seconds]`