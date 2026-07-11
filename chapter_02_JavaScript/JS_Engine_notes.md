How JS Engine Works

JS engine read, interprets & executes JS code
 
Step 1. Tokenizing | Laxical Analysis
        - JS engine first breaks raw code into small meaningful chunks called Token

Step 2. Parsing | Syntax Analysis
        - It presents grammatical structure of code
        - syntax error caught in this stage

Step 3. AST | Abstract Syntax Tree
        - Token converted into structured tree representing logic
        - engine breaks the code like keywaord, indentifiers, operators, values, punctuations

Step 4. Interpreter | Ignition
        - Ignition Creates lightweight bytecode from AST and starts executing immediately.

Step 5. Execution (Run Time with Call Stack)
	- Cold code being run here
	- Cold Code ->  simple the code which does not require Optimization

Step 6. Profiler + JIT Optimization
 	- Hot code being optimized & complied at this stage
        - Hot Code -> Code which has nexted lopps, call back, promises which needs Optimization
        - TurboFan / Compiler  -> it optimized Hot code & converts same to ByteCode.

Step 7. Garbage Collector 
	- It removes unused or unreachable objects automatially
	- It frees-up memory, prevents memory leaks & keeps performance efficient.

Step 8. Machine Code Execution
	- The final optimized code is executed directly by the CPU. 
	- This gives the best performance at runtime.

How to See the Bytecode? -> node --print-bytecode test.js

Source Code -> Human written code using IDE which is juman understandable
ByeCode -> An intermediate code created by the JavaScript engine, which humans cannot understand, 
Binary Code -> Also called machine code in 1010 understood by the real machines & chips 


