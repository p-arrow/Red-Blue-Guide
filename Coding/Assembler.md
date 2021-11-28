## TABLE OF CONTENTS
1. [SYNTAX](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#syntax)
2. [LITTLE ENDIAN BYTE ORDER](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#little-endian-byte-order)
3. [REGISTER AND FLAGS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#register-and-flags)
4. [COMMANDS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#commands)
5. [ADDRESSING METHODS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#addressing-methods)
6. [TERMS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#terms)
7. [C-APPLICATION ALLOCATION](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#c-application-allocation)
8. [FUNCTION CALL](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#function-call)
9. [CALLING CONVENTIONS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#calling-conventions)

<br />

### SYNTAX
1. AT&T
    - Command | Source | Destination: `addl $4, %esp`
    - Parameter size is indicated by last char
2. Intel
    - Command | Destination | Source: `add esp, 4`
    - Parameter size defined by register name

<br />

### LITTLE ENDIAN BYTE ORDER
- The bit with lowest value is saved first
- Example: hex 0x11223344 at address 0x504450
    -  `0x504450: 0x44`
    -  `0x504451: 0x33`
    -  `0x504452: 0x22`
    -  `0x504453: 0x11`

<br />

### REGISTER AND FLAGS
Parameter | Explanation
--------- | ------------
eax | Accumulator
ebx | Base
ecx | Counter
edx | Data
edi | Destination Index
esi | Source Index
ebp | Base Pointer
esp | Stack Pointer
eip | Instruction Pointer 
eflags | Status Register
CF | Carry Flag
PF | Parity Flag
ZF | Zero Flag
SF | Sign Flag
OF | Overflow Flag
IF | Interrupt Enable Flag

- 32 Bit OS: `eax`
- 64 Bit OS: `rax`

<br />

### COMMANDS
Command (Intel Syntax) | Meaning
---------------------- | -------
mov (dest, source) | copy data from source to dest; source does not change
add (dest, source) | adds source to dest and saves result in dest
sub (dest, source) | deduct source from dest and saves result in dest
div (dest, source) | Quotient saved in: `eax` ; Modulo saved in: `edx`
push (value) | put value on stack
pop (dest) | get last element from stack and put into dest
xor (dest, source) | XOR operation between source and dest and saves result in dest
call (dest) | calls function
leave | leave stack frame from current function
ret | terminate function
test (dest, source) | AND operation between source and dest and set flags (SF, ZF, PF); result discarded
cmp (dest, source) | compare source with dest and set flags
inc (dest) | increase dest by 1
dec (dest) | reduce dest by 1
lea | load effective address (performs register arithmetic)

<br />

### ADDRESSING METHODS
Method | Command | Meaning
------ | ------- | -------
Register Addressing | `mov eax, ebx` | Operation w/o access on memory
Immediate Addressing | `mov eax, [0x10]` | Operation w/o access on memory
Direct Addressing | `mov eax, 0x112233` | Register gets loaded with value of given memory address
Indirect Addressing | `mov eax, [ebx]` |  [ebx] is used as pointer; often used for arrays
Indexing | `mov eax, [ebx+5]` | addition of [ebx] and constant 5; the value of this newly calculated address gets loaded into eax

<br />

### TERMS
Name | Meaning
---- | -------
Byte | 8 Bit / 1 Byte
LWord | LongWord = 16 Bit = 2 Bytes
DWord | DoubleWord = 32 Bit = 4 Bytes
QWord | QuadWord = 64 Bit = 8 Bytes
TByte | 80 Bit = 10 Bytes
.cfi | call frame information pointer; points to previous frame
.cfa | canonical frame address
PIE | Position Independent Executable; for ASLR
PIC | Position Independent Code
PLT | Procedure Linkage Table; Table with called functions from other modules
LFB | Local Function Begin
LFE | Local Function End
ld | Linux Loader; `/usr/bin/ld`: link c++ file/libraries manually together (normally this is done automatically via g++)

<br />

### C-APPLICATION ALLOCATION
Field | Meaning
----- | -------
environment variables | command line parameter
stack | flexible size
heap | flexible size (storage of locale function variables)
bss | block started by symbol, fixed size, non-initialised variables
data | fixed size, initialised variables
text | compiled code

![grafik](https://user-images.githubusercontent.com/84674087/143775019-530c8b4f-7996-42e7-b6fe-129053491c46.png)
[Image Source](https://berbagidatapenting.blogspot.com/2020/02/data-structure-in-c-stack.html)

<br />

### FUNCTION CALL 

x86 Architektur
1) Function Prolog
--> Aktuelle Wert des ebp am Stack gesichert (Backup)
--> Aktuelle Wert des esp in ebp kopiert
--> Aktuelle Wert des esp wird verringert, damit lok. Var. Platz haben
2) Function Body
3) Function Epilog (Ergebnis in eax gespeichert)
--> leave: esp wird mit Wert des ebp geladen (akt. S-Frame verworfen)
--> ret: gesp. Rücksprungadresse vom Stack in eip geladen
--> Programmcode nach call-Befehl fortgesetzt

x86-64 Architektur
--> Ersten sechs Param d. Fkt in rdi/rsi/rdx/rcx/r8/r9 geladen
--> Erst ab siebten Param werden Werte auf Stack gelegt
--> eip wird auf Stack gespeichert (Rücksprungadresse)
--> Call-Befehl Ausführung, Adr der gewünschten Fkt in eip geladen
--> 128 Byte-Bereich unterhalb v. rsp ist reserviert (Red Zone)
--> Fkt kann Red Zone für temp. Daten verwenden
1) Function Prolog 
2) Function Body
3) Function Epilog (Ergebnis in rax gespeichert)

<br />

### CALLING CONVENTIONS
> Set rules on how arguments are passed to function and how values are returned from function. Herein "Caller" calls a function and "Callee"is called by a function.

#### Windows C-Applications
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
