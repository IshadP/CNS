---
title: Diffie Hellman
draft: false
date: 2025-09-09
obsidianUIMode: preview
tags:
  - Practicals
  - java
---


```Java
import java.util.*;

public class DiffieHellman{

    public static long powmod(long base, long power, long mod){
        if(power == 1) return base;
        return (((long)Math.pow(base, power)) % mod);
    }

   public static void DiffieHell(long g,long p,long a,long b){
    long x = powmod(g, a, p);
    long y = powmod(g, b, p);
    long ka = powmod(y, a, p);
    long kb = powmod(x, b, p);
    
    System.out.println("Secret Keys of A & B are: ");
    System.out.println(ka + " & " + kb);
    

    }
    public static void main(String[] args) {
        long publivg, publivp, privatea, privateb; 
        System.out.println("Ishad Pande | 25 | CSE");
         System.out.println("-----------------------------------");

        Scanner in = new Scanner(System.in);
        System.out.println("Enter the public number with user A(G)");
        publivg = in.nextInt();
        System.out.println("Enter the public number with user B(P)");
        publivp = in.nextInt();
        System.out.println("Enter the private Key for user A");
        privatea = in.nextInt();
        System.out.println("Enter the private key with user B");
        privateb = in.nextInt();
        System.out.println("-----------------------------------");
        DiffieHell(publivg, publivp, privatea, privateb);
    }
}
```
##### Output:
![[Pasted image 20250909111559.png]]