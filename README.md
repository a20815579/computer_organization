# single cycle RISC_V CPU
## main file discription
 - top_tb.v  
 Controlling all the program and verify the correctness of our CPU. The main features are as follows:  
    - send periodical signal CLK to CPU  
    - set the initial value of IM  
    - print the
    - value of DM, end the program.
- top.v  
The "top" module is the outmost module. It is responsible for connecting wires between CPU, IM and DM.  
Here are the wires:
    - instr_read : represents the signal whether the instruction should be read in IM.
    - instr_addr : represents the instruction address in IM.
    - instr_out : represents the instruction send from IM .
    - data_read : represents the signal whether the data should be read in DM.
    - data_write : has four signal , and every signal represents the byte of the data whether should be wrote in DM.
    - data_addr : represents the data address in DM.
    - data_in : represents the data which will be wrote into DM .
    - data_out : represents the data send from DM .
- SRAM.v  
SRAM.v is the abbreviation of "Instruction Memory" (or “Data Memory”). This module saves all the instructions (or data) and send instruction (or data) to CPU according to request.
![image](https://i.imgur.com/l5tRIWd.png)
- CPU.v  
CPU.v is responsible for connecting wires between modules. It can execute RISC_V instructions.  
Below is the block diagram  
![image](https://i.imgur.com/af3IQMm.jpg)

### other file discription
- memory layout
    ![image](https://i.imgur.com/qE9RGkA.png)
    - .text : Store instruction code.
    - .init & .fini : Store instruction code for entering & leaving the process.
    - .rodata : Store constant global variable.
    - .bss & .sbss : Store uninitiated global variable or global variable initiated as zero.
    - .data & .sdata : Store global variable initiated as non-zero
    - .stack : Store local variables
- setup.S  
This program start at “PC = 0”, execute function as followings:
    1. Reset register file
    2. Initial stack pointer and sections
    3. Call main function
    4. Wait main function return, then terminate program
- main.S  
This program start after setup.S, it will verify all RISC-V instructions (50 instructions).
- main.hex  
Using the cross compiler of RISC-V to compile test program, and write result in verilog format. So you do not need to compile above program again.