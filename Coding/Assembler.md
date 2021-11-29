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
10. [CODE EXAMPLES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Assembler.md#code-examples)

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
jmp | jump
je A, B | jump if equal
jne A, B | jump if not equal
jg A, B | jump if greater than
jge A, B | jump if greater or equal
jl A, B | jump if less than
jle A, B | jump if less or equal


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
stack | flexible size, storage of locale function variables, 
heap | flexible size 
bss | block started by symbol, fixed size, **uinitialised variables**
data | fixed size, **initialised variables**
text | compiled code

![grafik](https://user-images.githubusercontent.com/84674087/143775019-530c8b4f-7996-42e7-b6fe-129053491c46.png)

[Image Source](https://berbagidatapenting.blogspot.com/2020/02/data-structure-in-c-stack.html)

<br />

### FUNCTION CALL 
1. **x86 Architecture**
    - A) Function Prolog
        - Current value of `ebp` saved on stack (backup ebp)
        - Current value of `esp` copied into `ebp` (backup esp)
        - `esp` gets freed to allocate space for local variables
    - B) Function Body
    - C) Function Epilog (result saved in eax)
        - leave: `esp` gets loaded with value from `ebp` (recover esp from backup)
        - ret: saved return address is taken from stack and loaded into `eip` 
            - `pop eax`
            - `jmp eax` 
        - Main program code continues after call-command 

2. **x86-64 Architecture**
    - Pre-Steps:
        - First six parameters of function get loaded: `rdi` / `rsi` / `rdx` / `rcx` / `r8` / `r9`
        - From 7th parameter onwards values are pushed onto stack 
        - `eip` is saved on stack (return address)
        - The call command is executed and thus the function address gets loaded into `eip` 
        - 128 Byte area below `rsp` gets reserved (**Red Zone**)
        - The called function can use Red Zone for temporary data 
    - A) Function Prolog (like x86 Architecture)
    - B) Function Body (like x86 Architecture)
    - C) Function Epilog (like x86 Architecture, result saved in rax)

```
func:
    push ebp                ; PROLOGUE backup ebp
    mov ebp, esp            ; PROLOGUE backup esp
    sub esp, 2              ; PROLOGUE allocate space for variables
    mov [esp], byte 'H'
    mov [esp+1], byte 'i'
    mov eax, 4              ; sys_write system call
    mov ebx, 1              ; stdout file descriptor
    mov ecx, esp            ; pointer to bytes to write
    mov edx, 2              ; number of bytes to write
    int 0x80                ; perform system call
    mov esp, ebp            ; EPILOGUE recover esp 
    pop ebp                 ; EPILOGUE recover ebp 
    ret                     ; EPILOGUE terminate func and return to main stack
```

<br />

### CALLING CONVENTIONS
> Set rules on how arguments are passed to function and how values are returned from function. Herein "Caller" calls a function and "Callee"is called by a function.

#### Windows C-Applications
1. **cdecl** (default for C/C++ programms)
    - Passing order: Right to left
    - How: The calling function pops the arguments from the stack
    - Stack Cleanup: Caller
    - Compiler Option: /Gd
2. **stdcall** (default for Win32 API)
    - Passing order: Right to left
    - How: The called function pops its own arguments from the stack
    - Stack Cleanup: Callee
    - Compiler Option: /Gz

<br />

### CODE EXAMPLES

#### Hello World (written in assembler)
- `sudo apt install nasm`: The Netwide Assembler, a portable 80x86 assembler
- `nano ex2.asm`: write the code below
- `nasm -f elf32 ex2.asm -o ex2.o`: transform assembler code into object
- `ld -m elf_i386 ex2.o -o ex2`: build executable from object file with GNU linker ld
- `./ex2`

```
global _start

section .data
        msg db "Hello, world!", 0x0a    ; 0x0a = 10 = newline
        len equ $ - msg                 ; determine len_of_string by "sub string_end - string"

section .text
_start:                                 ; start label = entry point
        mov eax, 4                      ; sys_write system call 
        mov ebx, 1                      ; stdout file descriptor
        mov ecx, msg                    ; bytes to write (value)
        mov edx, len                    ; number of bytes to write
        int 0x80                        ; int = interrupt | 0x80 = system call = interrupt and perform sys_call, i.e. write string to stdout
        mov eax, 1                      ; sys_exit system call
        mov ebx, 0                      ; exit status is 0
        int 0x80                        ; perform system call, i.e. exit program successfully
```

#### Hello World (written in C/C++)
- `nano hello.c`: write code
- `gcc -Wall -g hello.c -o hello` / `g++ -Wall hello.cpp -o hello`: build binary "hello" from hello.c/hello.cpp
- `gdb hello` + `set disassembly intel` + `disass main`: debug binary "hello" and analyse assembly code

```
## CODE A (C)##

#include <stdio.h>
int main(){
        printf("Hello World!\n");
        return 0;
}

## CODE B (C++)##

#include <iostream>
using namespace std;
int main(){
        cout << "Hello World!" << endl;
        return 0;
}
```
```
# gdb output CODE A
Dump of assembler code for function main:
   0x0000000000001139 <+0>:     push   rbp
   0x000000000000113a <+1>:     mov    rbp,rsp
   0x000000000000113d <+4>:     lea    rax,[rip+0xec0]        # 0x2004
   0x0000000000001144 <+11>:    mov    rdi,rax
   0x0000000000001147 <+14>:    call   0x1030 <puts@plt>
   0x000000000000114c <+19>:    mov    eax,0x0
   0x0000000000001151 <+24>:    pop    rbp
   0x0000000000001152 <+25>:    ret    
End of assembler dump.


# gdb output CODE B
Dump of assembler code for function main:
   0x0000000000001169 <+0>:     push   rbp
   0x000000000000116a <+1>:     mov    rbp,rsp
   0x000000000000116d <+4>:     lea    rax,[rip+0xe90]        # 0x2004
   0x0000000000001174 <+11>:    mov    rsi,rax
   0x0000000000001177 <+14>:    lea    rax,[rip+0x2f02]        # 0x4080 <_ZSt4cout@GLIBCXX_3.4>
   0x000000000000117e <+21>:    mov    rdi,rax
   0x0000000000001181 <+24>:    call   0x1040 <_ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc@plt>
   0x0000000000001186 <+29>:    mov    rdx,QWORD PTR [rip+0x2e43]        # 0x3fd0
   0x000000000000118d <+36>:    mov    rsi,rdx
   0x0000000000001190 <+39>:    mov    rdi,rax
   0x0000000000001193 <+42>:    call   0x1050 <_ZNSolsEPFRSoS_E@plt>
   0x0000000000001198 <+47>:    mov    eax,0x0
   0x000000000000119d <+52>:    pop    rbp
   0x000000000000119e <+53>:    ret    
End of assembler dump.
```
#### Initialize Data
```
section .data
    ; db is 1 byte
    name1 db "string"
    name2 db 0xf6
    name3 db 100
    ; dw is 2 bytes
    name4 dw 1000
    ; dd is 4 bytes
    name5 is 10000
```

#### Jump Operation
- Assemble and link the code (ex4.asm) below
- `./ex4`
- `echo $?`: To verify the result saved in ebx
- Output: 16 (2^4)
```
global _start

section .text
_start:
        mov ebx, 1      ; start ebx at 1
        mov ecx, 4      ; number of iterations
label:
        add ebx, ebx    ; ebx += ebx
        dec ecx         ; ecx -= 1
        cmp ecx, 0      ; compare ecx with 0
        jg label        ; jump to label if greater
        mov eax, 1      ; sys_exit system call
        int 0x80
```

#### Fill ESP manually, then stdout

```
global _start

_start:
        sub esp, 5
        mov [esp], byte 'H'
        mov [esp+1], byte 'e'
        mov [esp+2], byte 'y'
        mov [esp+3], byte '!'
        mov [esp+4], byte 0x0a  ; 0x0a = newline
        mov eax, 4              ; sys_write system call
        mov ebx, 1              ; stdout file descriptor
        mov ecx, esp            ; pointer to bytes to write
        mov edx, 5              ; number of bytes to write
        int 0x80                ; perform system call
        mov eax, 1              ; sys_exit system call
        mov ebx, 0              ; exit status 0
        int 0x80
```

#### Calling C functions with x86 assembly
- `nano ex10.asm`: write code (as below)
- `sudo apt install gcc-multilib`: You may have to install multilib package in the first place to run 32bit executable on your 64bit machine
- `nasm -f elf32 ex10.asm -o ex10.o && gcc -m32 ex10.o -o ex10`: assemble and build ex10
- `./ex10`
- Output: Testing 123...
```
global main 
extern printf                           ; mark "printf" as external 

section .data 
    msg db "Testing %i...", 0x0a, 0x00  ; 0x0a = newline | 0x00 string termination

section .text
main:
    push ebp                            ; prologue
    mov ebp, esp                        ; prologue
    push 123                            ; function paramter (pass in reverse order: %i msg printf())
    push msg
    call printf
    mov eax, 0                          ; exit status 0
    mov esp, ebp                        ; epilogue
    pop ebp                             ; epilogue
    ret    
```
