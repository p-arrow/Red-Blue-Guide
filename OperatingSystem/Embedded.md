# TABLE OF CONTENTS
1) [GLOSSARY](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Embedded.md#glossary)
2) [INTERFACES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Embedded.md#interfaces)
3) [SECURE BOOT](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Embedded.md#secure-boot)

<br />

# GLOSSARY
- **PSCI**: Power State Control Interface
- **BL**: Boot Loader	
- **Flash**:
  - Code flash : The ROM area where program code is written
  - Data flash : The ROM area where data is written 
- **PCB**: Printed Circuit Board
- **HAB**: High Assurance Boot
- **DMA**: Direct Memory Access
  - Potentially risky if untrusted, e.g. USB3 can use DMA
- **MPU**: Micro Processor Unit
  - Contain only a CPU, and therefore require added peripherals to perform tasks
- **MCU**: Micro Controller Unit
  - Contain RAM, ROM, and similar peripherals, which allow them to perform (simple) tasks independently
- **SoC**: System-on-a-Chip
  - Refers to MCUs with a greater number of onboard peripherals and functionality
  - Integrates funcionality of multiple logical controller
- **SPI**: Serial Peripheral Interface
  - For short-distance communication between microcontroller and peripheral IC, primarily in embedded systems
- **I2C**: Inter-Integrated Circuit
- **GPIO**: General Purpose I/O
- **SRAM** (Static RAM):
   - It relies on static flip-flops to store data
   - Therefore, the information stored in SRAM can be retained for a long time without power failure and no additional circuit refresh is required
   - It requires about six transistors for a memory cell, which makes it high-cost, small-capacity, and high-speed
   - Therefore, it is often used as the primary cache or secondary cache of the CPU
- **DRAM** (Dynamic RAM): 
   - It uses capacitors to store information (charge), but any capacitor has leakage (charge loss), so the stored information will be lost
   - To solve this problem, DRAM needs to read and rewrite (so-called refresh) the DRAM at regular intervals (2ms)
   - It requires about one transistor and one capacitor for a memory cell
   - Low-cost and large-capacity, but it needs to be refreshed and the speed is slower than SRAM
   - Therefore, it is often used as the main memory of the computer
- **ADRAM** (Asynchronous DRAM):
   - In ADRAMs, the system clock doesn't coordinate or synchronize memory access
   - Therefore, there is delay in the response of the memory
- **SDRAM** (Synchronous DRAM):
   - In SDRAMs, the system clock coordinates or synchronizes memory access
   - Therefore, the CPU knows the timing or the exact cycle number of the available data of the RAM, the input bus, and the output bus
   - Improves the read and write speed of the memory
- **DDR SDRAM** (Double-Data-Rate SDRAM):
   - DDR SDRAM is based on SDRAM
   - SDRAM transmits data only once in a clock cycle and it usually transmits data in the rising period of the clock
   - As for DDR SDRAM, it transmits data twice in a clock cycle and it can transmit data once in the rising and falling periods of the clock, respectively
- **PLC** (Programmable Logic Controller) 
  - A computer designed for industrial area
  - Can automate and monitor mechanical systems
  - PLC firmware can be patched to fix vulns
  - Patch maybe once a year (not frequently!)
- **RTOS** (Real-Time Operating System)
  - OS that prioritizes deterministic execution of operations for time-critical tasks
- **FPGA** (Field Programmable Gate Array)
  - Processor can be programmed for specific function by customer (i/o manufacturer)
- **CAN** (Controller Area Network)
  - To connect subsystems
  - CAN concept originates from 80s/90s
  - No security included back these days (!)
  - No source addressing / message authen in CAN (!)
- **ICS** (Industrial Control Systems)
  - A NW that manages embedded devices
  - Uses Fieldbus to link PLCs within an OT network
  - HMI (Human Machine Interface) on a PLC
  - Data Historian: Software that aggregates/catalogs data within ICS
  - **Operational Technology prioritize availability and integrity over confidentiality (!)**
- **SCADA** (Supervisory Control and Data Acquisition)
  - Type of ICS that manages large-scale multiple-site devices
- **Modbus**
  - Communication protocol used in OT network (proprietary)
  - It's alike TCP, but for OT
  - Provides ability to query and change configs of each PLC
- **NIST-82**: Guide to Industrial Control Systems
   - Establish administrative control over OT
   - Implement minimum network links (disable services/protocols )
   - Develop/Test patch management for OT networks
   - Perform regular audits
   - Vuln scanners can cause problems to OT NWs (!)
   - Better: Passive Analysis



<br />

# INTERFACES

<br />

# SECURE BOOT
## BOOT LOADER
- [https://github.com/mcu-tools/mcuboot/blob/master/docs/design.md](https://github.com/mcu-tools/mcuboot/blob/master/docs/design.md)
- [https://github.com/mcu-tools/mcuboot/blob/master/docs/encrypted_images.md](https://github.com/mcu-tools/mcuboot/blob/master/docs/encrypted_images.md)
- [https://github.com/mcu-tools/mcuboot/blob/master/docs/signed_images.md](https://github.com/mcu-tools/mcuboot/blob/master/docs/signed_images.md)

### Flash Map
- A device's flash is partitioned according to its flash map
- At a high level, the flash map maps numeric IDs to flash areas
- A flash area is a region of disk with the following properties:
   - An area can be fully erased without affecting any other areas
   - A write to one area does not restrict writes to other areas

### Image Slots
- Flash memory can be partitioned into multiple image areas
- Each contains two image slots: a primary slot and a secondary slot
- Normally, the boot loader will only run an image from the primary slot
- If the boot loader needs to run the image in the 2nd slot, it must copy its contents into the primary slot
- Either by swapping the two images or by overwriting the contents of the primary slot
- The boot loader requires a scratch area to allow for reliable image swapping
- The scratch area must have a size that is enough to store at least the largest sector that is going to be swapped
- Many devices have small equally sized flash sectors, e.g. 4K
- Others have variable sized sectors where the largest sectors might be 128K or 256K
- Main reason for using a larger size for the scratch is that flash wear will be more evenly distributed

### Upgrade Modes
#### Overwrite
- Before the new firmware image is executed, the entire contents of the primary slot are overwritten with the contents of the secondary slot
- **Pros**
   - Fail-safe and resistant to power-cut failures.
   - Less memory overhead, with a smaller MCUboot trailer and no scratch area.
   - Encrypted image support available when using external flash.
- **Cons**
   - Does not support pre-testing of the new image prior to overwrite.
   - Does not support automatic application fallback mechanism.

#### Swap
- Contents of the primary slot and the secondary slot will be swapped
- The new image will then start from the primary slot
- **Pros**
   - The bootloader can revert the swapping as a fallback mechanism after a faulty update
   - The application can perform a self-test to mark itself permanent.
   - This image upgrade mode is fail-safe and resistant to power-cut failures.
   - Encrypted image support is available when using external flash.
- **Cons**
   - Need to allocate a scratch area
   - Larger memory overhead, due to a larger image trailer and additional scratch area.
   - Larger number of write cycles in the scratch area, faster wearing out of scratch sectors

#### Direct Execute-in-Place (XIP)
- Two firmware update images must be generated
- One of them is linked to be executed from the primary slot memory region, and the other is linked to be executed from the secondary slot
- **Pros**
   - Faster boot time, as there is no overwrite or swap of application images needed
   - Fail-safe and resistant to power-cut failures.
- **Cons**
   - Added application-level complexity to determine which firmware image needs to be downloaded
   - Encrypted image support is not available

#### RAM loading firmware update
- This update mode selects the newest image by reading the image version numbers in the image headers
- However, instead of executing it in place, the newest image is copied to RAM for execution
- The load address (the location in RAM where the image is copied to) is stored in the image header
- This upgrade method is typically not used in MCU environment
- **Cons**
   - Lower execution speed → image is exposed to attacks
   - Only the single image boot supported
   - Encrypted image support is not available


### Integrity Check
- During the integrity check, the boot loader verifies the following aspects of an image:
   - **32-bit magic number** must be correct (IMAGE_MAGIC)
   - Image must contain an **image_tlv_info struct**, identified by its magic (IMAGE_TLV_PROT_INFO_MAGIC or IMAGE_TLV_INFO_MAGIC) exactly following the firmware (hdr_size + img_size)
   - Image must contain a **SHA256 TLV**: Calculated SHA256 must match SHA256 TLV contents
   - Image may contain a **signature TLV**. If it does, it must also have a KEYHASH TLV with the hash of the key that was used to sign

### Signature Check
- The whole public key is embedded in the bootloader code and its hash is added to the image manifest as a KEYHASH TLV entry
- During boot the public key is validated before using it for signature verification

### Downgrade prevention 
- A feature which enforces that the new image must have a higher version/security counter number than the image it is replacing
- This prevents the malicious downgrading of the device to an older and possibly vulnerable version of its firmware

### Encrypted Images
- Provide confidentiality of image data in transport (to the device) or while residing on an external flash
- When encrypting an image, **only the payload is encrypted**
- The image header needs to flag this image as ENCRYPTED (0x04) and a TLV with the key in the image
- The image will be automatically decrypted (after validation) during upgrade
- In Swap Mode: The primary image, also having the ENCRYPTED flag set and the TLV present, is re-encrypted while swapping to the 2nd slot

## THREAT
### Secure Boot Process (High Level)
- Boot loader has embedded pubkey
- Boot loader loads image which contains code + signature + pubkey-hash
- Boot loader computes hash of embedded pubkey and compares it with pubkey-hash from image
- If valid, boot loader will use its embedded pubkey to decrypt the signature
- Boot loader will compute a hash of the image code and compares it with the decrypted hash of the signature
- If valid, boot loader will boot the image in the primary slot

### Attacker's targets during Boot Sequence
- Boot Code (stored on ROM/Flash)
- Keys (for boot code decryption)
- Cryptographic engines (secure HW)

### Attack Surface
- Hash Comparison (stored hash vs. calculated hash)
- If Secure Verification Fail -> Infinite Loop started
   - Timing is not an issue for attacker anymore!
   - Typical Smart card Attack
   - Better to reset/wipe keys 

### Best Practice
- Implement double checks (verification) within your code, to avoid single point of failure
- Compiler Optimization is used to decrease code size in ROM
   - Avoid unintended compiler problems by using `volatile`
   - Check the code **AFTER** it got compiled and verify its correctness 
- Minimize Attack Surface:
   - Authenticate all code and data 
   - Limit functionality in ROM code
   - Disable memories when not required
- Measured Boot: Gathers secure metrics to validate and attest it in a report
- eFuse:
   - Permanently alter the state of a transistor on a computer chip
   - Emergency solution in case of compromise 
