## CODE SNIPPETS

### XOR OPERATION
```
public class Decrypt
{
  public static void main(String[] args) {
    System.out.println(decrypt("\005\006\006\003U\001UU\031WQ\f\006\031\000PU\f\031\rVU\002\031W\000\rQ\f\004\rVU\003\006\004", (byte)52));
  }
    public static String decrypt(String paramString, byte paramByte) {
      byte[] arrayOfByte2 = paramString.getBytes();
      byte[] arrayOfByte1 = new byte[arrayOfByte2.length];
      for (byte b = 0; b < arrayOfByte2.length; b++)
        arrayOfByte1[b] = (byte)(byte)(arrayOfByte2[b] ^ paramByte);
      return new String(arrayOfByte1);
    } 
}
```
