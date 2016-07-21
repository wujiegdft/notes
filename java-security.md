- [The java.security Package](http://docstore.mik.ua/orelly/java-ent/jnut/ch17_01.htm)
- 

```java
byte[] bytes = Base64.decodeBase64(privateKey.getBytes("UTF-8"));
PKCS8EncodedKeySpec pkcs = new PKCS8EncodedKeySpec(bytes);
KeyFactory factory = KeyFactory.getInstance(KEY_RSA);
PrivateKey key = factory.generatePrivate(pkcs);
Signature signature = Signature.getInstance(KEY_RSA_SIGNATURE);
signature.initSign(key);
signature.update(data);
str = Base64.encodeBase64String(signature.sign());
```

```java
// 解密由base64编码的公钥
byte[] bytes = Base64.decodeBase64(publicKey.getBytes("UTF-8"));
X509EncodedKeySpec keySpec = new X509EncodedKeySpec(bytes);
KeyFactory factory = KeyFactory.getInstance("RSA");
PublicKey key = factory.generatePublic(keySpec);
// 用公钥验证数字签名
Signature signature = Signature.getInstance("SHA256withRSA");
signature.initVerify(key);
signature.update(data);
flag = signature.verify(Base64.decodeBase64(sign));
```
