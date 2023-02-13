This instruction should be used to waste a standard instruction cycle length. This could be used to create real time delays without putting extra load on the processor. This instruction will not interact with storage units, memory, registers, or any other resources of such that store data. This instruction will continue as a normal operation. Operations executed after this should be expected to run normally, no influence will be created by this.

# Signature
```rxarch
NoOperation();
```

# Usage as Delay
```rxarch
[Static]:
int iterations;

[Executable]:
Main:
	JumpIfEqual(iterations, 300, &AfterFinish);
	NoOperation();
	Add(iterations, 1);
	Jump(&Main); // 4 instructions for each cycle of `Main`
	
AfterFinish:
	Kill();
```

The programs time can be determined by determining the number of instructions executed. It can be solved by performing $t = \frac{1}{f} * i + o$.
 - `t`: Time elapsed in seconds.
 - `f`: Frequency of the core clock.
 - `i`: Instructions that were executed for the delay.
 - `o`: Offset operations, such as instructions that costed an instruction cycle outside the `Main` function.

**Solution**
$13 = \frac{1}{1000} * (4 * 299) + 1$.
