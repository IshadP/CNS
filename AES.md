---
title: AES
draft: false
date: 2025-09-02
view: read
tags:
  - Practicals
  - java
---
```Java
// paste code here
import java.nio.charset.StandardCharsets;
import java.security.spec.KeySpec;
import java.util.Base64;
import javax.crypto.Cipher;
import javax.crypto.SecretKey;
import javax.crypto.SecretKeyFactory;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.PBEKeySpec;
import javax.crypto.spec.SecretKeySpec;

public class AES {

    private static final String SECRET_KEY = "fkdjfjajlkgjoaojgoaajfoajoiu";
    private static final String SALT = "fdljfjafjlajffkajf";

    public static String encrypt(String strToEncrypt) {
        try {
            byte[] iv = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
            IvParameterSpec ivspec = new IvParameterSpec(iv);

            SecretKeyFactory factory = SecretKeyFactory.getInstance("PBKDF2WithHmacSHA256");
            KeySpec spec = new PBEKeySpec(SECRET_KEY.toCharArray(), SALT.getBytes(), 65536, 256);
            SecretKey tmp = factory.generateSecret(spec);
            SecretKeySpec secretKey = new SecretKeySpec(tmp.getEncoded(), "AES");

            Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
            cipher.init(Cipher.ENCRYPT_MODE, secretKey, ivspec);

            return Base64.getEncoder().encodeToString(
                    cipher.doFinal(strToEncrypt.getBytes(StandardCharsets.UTF_8))
            );
        } catch (Exception e) {
            System.out.println("Error while encrypting: " + e);
        }
        return null;
    }

    public static String decrypt(String strToDecrypt) {
        try {
            byte[] iv = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
            IvParameterSpec ivspec = new IvParameterSpec(iv);

            SecretKeyFactory factory = SecretKeyFactory.getInstance("PBKDF2WithHmacSHA256");
            KeySpec spec = new PBEKeySpec(SECRET_KEY.toCharArray(), SALT.getBytes(), 65536, 256);
            SecretKey tmp = factory.generateSecret(spec);
            SecretKeySpec secretKey = new SecretKeySpec(tmp.getEncoded(), "AES");

            Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
            cipher.init(Cipher.DECRYPT_MODE, secretKey, ivspec);

            return new String(
                    cipher.doFinal(Base64.getDecoder().decode(strToDecrypt)),
                    StandardCharsets.UTF_8
            );
        } catch (Exception e) {
            System.out.println("Error while decrypting: " + e);
        }
        return null;
    }

    public static void main(String[] args) {

        System.out.println("Ishad Pande, 25, B2");
        System.out.println("------------------");

        String originalString = "IshadSanjivPande";
        System.out.println("Plain Text: " + originalString);

        String encryptedString = encrypt(originalString);
        System.out.println("Cipher Text: " + encryptedString);

        String decryptedString = decrypt(encryptedString);
        System.out.println("Plain Text: " + decryptedString);
    }
}

```
##### Output:

![[Pasted image 20250902090505.png]]
