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
