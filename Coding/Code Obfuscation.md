# Red Team

<br />

## Methods 
1. **Identifier Renaming**: Bezeichner umbenennen
2. **Diversifying**: Arithmetische Operationen umformen
3. **Reordering**: Neuordnung von Code
4. **Splitting & Merging**: von Codeblöcken 
5. **Copying Code**: Codemenge aufblähen
6. **Interpretation**: Teil des Codes während Laufzeit v. Interpreter verarbeiten lassen (Performance Einbuße!)
7. **Compression**: UPX (Ultimate Packer for Executables), FOSS @ Sourceforge

## tools
- **ProGuard**
  - [https://github.com/Guardsquare/proguard](https://github.com/Guardsquare/proguard)
  - [https://en.wikipedia.org/wiki/ProGuard](https://en.wikipedia.org/wiki/ProGuard)
- **Msfvenom**
  - [Own Notes about Msfvenom](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Wiki/Applications/Msfvenom%20(Payload%20Generator).md)
  - [https://github.com/g0tmi1k/msfpc](https://github.com/g0tmi1k/msfpc)

<br />

# Blue Team

<br />

## Best Practice (Software Development)
1. Deploy software without debugging information
2. Obfuscate code before it is shared with customers/users 
3. Do not hard code any sensitive data into your code (!) 
