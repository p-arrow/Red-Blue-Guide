# RedTeam

## Attack Vectors
- **Code Injection / XSS**: Insert malicious data - unvalidated user controlled data - into a log file
- **Log Forging Attack**: Insert abitrary data (dummy logs) into log file to a) cover attacker's tracks and b) manipulate the log integrity
- **Denial of Service**: If data can be directly injected, an extraordinary amount of data could lead to crashes (lack of memory)


<br />

# BlueTeam

## Best Practice
- **Blocking**: Block critical characters like `\r`, `\n`, `< > % / ' "` (may require too much performance of your system !)
   -  `\r` = carriage return
   -  `\n` = newline
- **Encoding**: Escape critical characters like `\r`, `\n`, `< > % / ' "` (less performance consumption)
- Normalize your log files (uniform encoding to get uniform pattern) before you remove parts of it
- Use only encoded HTTP-Request-Parameters in your log file 
