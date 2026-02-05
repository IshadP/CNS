```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import java.util.Base64;
import java.util.Scanner;

public class p4 {

    public static void main(String[] args) {
        try (Scanner scanner = new Scanner(System.in)) {

            // Take input from user
            System.out.print("Enter the text to encrypt: ");
            String text = scanner.nextLine();

            // Generate DES key
            KeyGenerator keyGen = KeyGenerator.getInstance("DES");
            SecretKey secretKey = keyGen.generateKey();

            // Encrypt the text
            String encryptedText = encrypt(text, secretKey);
            System.out.println("Encrypted Text: " + encryptedText);

            // Decrypt the text
            String decryptedText = decrypt(encryptedText, secretKey);
            System.out.println("Decrypted Text: " + decryptedText);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static String encrypt(String data, SecretKey key) throws Exception {
        Cipher cipher = Cipher.getInstance("DES/ECB/PKCS5Padding");
        cipher.init(Cipher.ENCRYPT_MODE, key);
        byte[] encryptedBytes = cipher.doFinal(data.getBytes());
        return Base64.getEncoder().encodeToString(encryptedBytes);
    }

    public static String decrypt(String encryptedData, SecretKey key) throws Exception {
        Cipher cipher = Cipher.getInstance("DES/ECB/PKCS5Padding");
        cipher.init(Cipher.DECRYPT_MODE, key);
        byte[] decryptedBytes = cipher.doFinal(Base64.getDecoder().decode(encryptedData));
        return new String(decryptedBytes);
    }
}

```