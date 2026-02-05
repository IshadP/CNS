---
title: SHA Algorithm
draft: false
date: 2025-10-07
obsidianUIMode: preview
tags:
- 
---

```Java
import java.security.MessageDigest;
import java.util.Scanner;

public class SHA {

    // Method to compute SHA hash
    public static String hash(String input, String algorithm) throws Exception {
        MessageDigest digest = MessageDigest.getInstance(algorithm);
        byte[] hashBytes = digest.digest(input.getBytes("UTF-8"));

        // Convert to hexadecimal string
        StringBuilder hexString = new StringBuilder();
        for (byte b : hashBytes) {
            String hex = Integer.toHexString(0xff & b);
            if (hex.length() == 1)
                hexString.append('0');
            hexString.append(hex);
        }
        return hexString.toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
             System.out.println("Ishad Pande, 25, B2");
             System.out.println("------------------");
             System.out.println("SHA Algorithm");
            System.out.print("Enter text to hash: ");
            String input = scanner.nextLine();

            System.out.print("Enter SHA algorithm (SHA-1 / SHA-256 / SHA-384 / SHA-512): ");
            String algorithm = scanner.nextLine().toUpperCase();

            String hashed = hash(input, algorithm);
            System.out.println("\n[" + algorithm + " Hash]");
            System.out.println(hashed);

        } catch (Exception e) {
            System.err.println("Error: " + e.getMessage());
        }

        scanner.close();
    }
}


```
##### Output:
![[Pasted image 20251007222948.png]]