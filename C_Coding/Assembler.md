## Assembler Code

#### Syntax
1. AT&T
    - Source before Destination
    - Parameter size is indicated by last char
    - Exp: `addl $4, %esp`
2. Intel
    - Destination before Source
    - Parameter size defined by register name
    - Exp: `add esp, 4`

#### Register and Flags

Parameter | Explanation
--------- |------------
edx | Data
edi | Destination Index
esi | Source Index
ebp | Base Pointer
esp | Stack Pointer
eip | Instruction Pointer 
CF | Carry Flag
PF | Parity Flag
ZF | Zero Flag
SF | Sign Flag
OF | Overflow Flag
IF | Interrupt Enable Flag

#### Terms
- LWord (LongWord) = 16 Bit
- DWord (DoubleWord) = 32 Bit
- QWord (QuadWord) = 64 Bit
- .cfi (call frame information pointer): points to previous frame
- .cfa: canonical frame address
- PIE (Position Independent Executable): for ASLR
- PIC (Position Independent Code)
- PLT (Procedure Linkage Table): Table with called functions from other modules
- LFB (Local Function Begin)
- LFE (Local Function End)
- ld (Linux Loader):
    - `/usr/bin/ld`
    - link c++ file/libraries manually together
    - Normally this is done automatically via g++

#### Calling Convention
> Set rules on how arguments are passed to function and how values are returned from function. Herein "Caller" calls a function and "Callee"is called by a function.

**Windows C-Applications**
1. cdecl (default for C/C++ programms)
    - Passing order: Right to left
    - How: The calling function pops the arguments from the stack
    - Stack Cleanup: Caller
    - Compiler Option: /Gd

2. stdcall (default for Win32 API)
    - Passing order: Right to left
    - How: The called function pops its own arguments from the stack
    - Stack Cleanup: Callee
    - Compiler Option: /Gz
