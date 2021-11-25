**Buffer Overflow**: *When a process stores data outside the memory range allocated by the developer*

**Stack**: *Reserved area of memory where program saves return address when function call received. With buffer overflow, the return pointer is overwritten with attackers code*

# Red Team

## Stack Overflow vs. Heap Overflow
- Stack overflow is simpler than Heap overflow: C/C++ often use stack-based memory allocation techniques (!)

## Best Practices

### Determine Buffer Size
- Generate a uniqe string with metasploit
   - `usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 700`: Create string length of 700 bytes
   - `usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -q [EIP Value]`: get offset; extract [EIP value] from debugger during buffer overflow

## Examples

### Python Script for Buffer Overflow

```
#To make you life easier import struct for automatic little-endian byte writing style
import struct

# \x41 = A
Buffer = "\x41" * 50
# Debugger: Search the address of EIP or use JMP ESP
EIP = struct.pack("I", 0xbffff780)
NOP = "\x90" * 16
shellcode = "\x31\xc0\....\x31\x80"

print(Buffer + EIP + NOP + shellcode)
```

### DEP Bypass via Return-to-libc

1. Use BufferOverflow to overwrite RET Address with system() 
2. Until this point no need of code execution on stack (= DEP Bypass)
3. Without ASLR: Static address of system() sufficient
4. With ASLR: Call system() address with offset 
5. Transfer paramaters to system(): Attention to calling convention (!)
    - Option A) prepare arguments on stack 
    - Option B) prepare arguments in registers 
6. Input dummy RET address for (not needed) return from system()
7. The address field contains pointer to string "/bin/sh" (i/o command)

![grafik](https://user-images.githubusercontent.com/84674087/132368710-d35cd92c-580f-408b-a5c1-56eb3f03d059.png)



# BlueTeam

#### 1) ASLR (Address Space Layout Randomization)
- Introduced with Win XP SP3 (randomizes first two Bytes)
- Changes Base Address of loaded DLL/Stack/Heap after reboot
- Generally activated in Linux 
- Linux/CLI:
   - `echo 0 > /proc/sys/kernel/randomize_va_space` (deactivate)
   - `echo 1 > /proc/sys/kernel/randomize_va_space` (partly activate)
   - `echo 2 > /proc/sys/kernel/randomize_va_space` (activate)
   - Alternatively: `sysctl -a --pattern randomize kernel.randomize_va_space = 0/1/2`

#### 2) Stack Cookie/Stack Canary
- Placed between locale variables and RET-Befehl 
- System verifys if Canary has been destroyed due to Buffer Overflow
- Linux/Compiler: `gcc [...] -f no-stack-protector` (for deactivation)
- Windows/VisualStudio: `/GS` (activate via linker)

#### 3) SafeSEH
- Introduced with WinVS 2013
- Provides list of valid SEH-addresses
- Verifies validity of handler address before call 
- Windows/VisualStudio: `/SAFESEH` (activate via linker)

#### 4) SEHOP (SEH Overwrite Protection)
- Verify during runtime, whether OS Default Handler is available 
- Windows: `HKLM\SYSTEM\CurrentControlset\Control\Session Manager\kernel\DisableExceptionChainValidation`
   - (Activation: 0 / Deactivation: 1)

#### 5) DEP (Data Execution Prevention)
- Introduced with Windows XP SP3
- Generally activated in Linux
- Win/CLI: `bcdedit /set nx` (Choose between AlwaysOn/OptOut/OptIn/AlwaysOff)
- Linux/Compiler: `gcc [...] -z executestack` (for deactivation)

#### 6) Heap Spraying
- Modern Browser have diverse protection mechanisms implemented 
   1. Nozzle:
      - Detection of program code (because normally only data or addresses)
   2. Bubble:
      - Detection of returning memory areas
   3. EMET (Enhanced Mitigation Experience Toolkit):
      - Pre-Allocation of cyclic addresses (prevents access via Head Spraying)

#### 7) Static Code Analysis

#### 8) Java, Python and PHP can detect overflow conditions
