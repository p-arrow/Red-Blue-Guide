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

### XML EXTERNAL ENTITY (Prevention)
```
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();

        //REDHAT
        //https://www.blackhat.com/docs/us-15/materials/us-15-Wang-FileCry-The-New-Age-Of-XXE-java-wp.pdf
        factory.setAttribute(XMLConstants.FEATURE_SECURE_PROCESSING, true);
        factory.setAttribute(XMLConstants.ACCESS_EXTERNAL_DTD, "");
        factory.setAttribute(XMLConstants.ACCESS_EXTERNAL_SCHEMA, "");

        //OWASP
        //https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html
        factory.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
        factory.setFeature("http://xml.org/sax/features/external-general-entities", false);
        factory.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
        // Disable external DTDs as well
        factory.setFeature("http://apache.org/xml/features/nonvalidating/load-external-dtd", false);
        // and these as well, per Timothy Morgan's 2014 paper: "XML Schema, DTD, and Entity Attacks"
        factory.setXIncludeAware(false);
        factory.setExpandEntityReferences(false);

        DocumentBuilder builder = factory.newDocumentBuilder();
```

### AES-CBC DECRYPTION BRUTEFORCE
- SecretKey derived from pin only
```
import java.util.Base64;
import java.security.MessageDigest;
import javax.crypto.Cipher;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.SecretKeySpec;


public class android07
{
  public static void main(String[] args){
    String s = "ED1nf3uLW4Hkwr1aGw+NpN5sgcRMPCFuk0XgtW181m4o6d0Ml3D/j6h1NSyOh4dbcGsbK6rcZOUyzHxWVb4QkA==";
    for (int i=0; i<9999; i++){
      try {
        byte[] enc = Base64.getDecoder().decode(s);
        String pin = String.format("%04d",i);
        byte[] iv = new byte[16];
        System.arraycopy(enc, 0, iv, 0, 16);
        IvParameterSpec ivp = new IvParameterSpec(iv);
        int z = enc.length - 16;
        byte[] data = new byte[z];
        System.arraycopy(enc, 16, data, 0, z);
        MessageDigest messageDigest = MessageDigest.getInstance("MD5");
        messageDigest.update(pin.getBytes("UTF-8"));
        byte[] key = new byte[16];
        System.arraycopy(messageDigest.digest(), 0, key, 0, 16);
        SecretKeySpec keys = new SecretKeySpec(key, "AES");
        Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        cipher.init(2, keys, ivp);
        String result = new String(cipher.doFinal(data));
        System.out.println(result);
      }
      catch (Exception exception) {
      }
    }
  }
}
```
- SecretKey derived from pin and string

```
import java.util.Base64;
import java.security.MessageDigest;
import javax.crypto.Cipher;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.SecretKeySpec;


public class android08
{
  public static void main(String[] args){
    String s = "G38zckAufW4B9A6sywz28kzgW8CCx1UWugLUTjKlo/kwV1CVesmr0tPX/JZOW0aik0TlkrcAIZZ/G0BigUtmeg==";
    String ptl = "<=== P3nt3st3rL4b ===>";
    for (int i=0; i<9999; i++){
      try {
        byte[] enc = Base64.getDecoder().decode(s);
        String pin = String.format("%04d",i);
        byte[] iv = new byte[16];
        System.arraycopy(enc, 0, iv, 0, 16);
        IvParameterSpec ivp = new IvParameterSpec(iv);
        int z = enc.length - 16;
        byte[] data = new byte[z];
        System.arraycopy(enc, 16, data, 0, z);
        MessageDigest messageDigest = MessageDigest.getInstance("MD5");
        messageDigest.update(ptl.getBytes("UTF-8"));
        messageDigest.update(pin.getBytes("UTF-8"));
        byte[] key = new byte[16];
        System.arraycopy(messageDigest.digest(), 0, key, 0, 16);
        SecretKeySpec keys = new SecretKeySpec(key, "AES");
        Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        cipher.init(2, keys, ivp);
        String result = new String(cipher.doFinal(data));
        System.out.println(result);
      } catch (Exception exception) {

      }
    }
  }
}
```
