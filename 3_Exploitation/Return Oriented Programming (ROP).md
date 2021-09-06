# RedTeam

## Charakteristic
1. Build up code from gadgets (fragments)
2. The code itself resides in unprotected memory area, i.e. called functions 
3. The code flow is controlled with RET-Addresses (return) on stack
4. The stack serves as storage for values and RETs 

**> Neutral ROP Chain**

![grafik](https://user-images.githubusercontent.com/84674087/132259755-bbdcca99-2e4b-47c0-8bf5-24ccb773c77e.png)


## Attention
1. ROP Gadgets should not affect ESP (PUSH/POP !)
2. ROP Gadgets are immutable (one can only use available code fragments)
3. Use only non-disruptive FILLER as ROP (avoid for instance `0x00 0x0d 0x0a` !)

**> Non-ideal ROP Chain**

![grafik](https://user-images.githubusercontent.com/84674087/132259625-bb507432-e389-4187-a3c3-e868858cdbe5.png)



## Exploit Structure
1. Place shellcode on stack
2. Deactivate DEP by leveraging VirtualAlloc function by using ROPs
3. Invoke and execute shellcode

**> Windows: VirtualAlloc() and VirtualProtect() can deactivate DEP during runtime (!)**

![grafik](https://user-images.githubusercontent.com/84674087/132259515-7b673d06-8373-4a81-8c08-b19ef776f13b.png)


## Advices
1. ImmunityDebugger: `!mona rop/ropfunc -n -o` > delivers rop_suggestions.txt
    - n = no Nullbytes
    - o = no module from OS
2. If you need to offset a value that contains nullbytes -> summand disassembly 
    - Exp: 0xBBBBBDEC + 0x44444444 = 0x230
3. The expression `DWORD PTR DS: [EAX]` means: -> Follow the pointer of the value stored in EAX
4. Fill up with `NOPS = "\x90" * 16` if needed
5. Set a specific register back to zero: `XOR EDX, EDX # RETN` (in this example EDX)
6. The value -1 written in hexadecimal: 0xFFFFFFFF
7. If no suitable code fragment is avaiable, then consider opcode from another operation as alternative for your ROP chain

**> Hidden PUSHAD (0x60) inside another opcode: 0x10041588**

![grafik](https://user-images.githubusercontent.com/84674087/132259454-f751e93f-b991-45e3-b6e4-508b933ee4cb.png)

