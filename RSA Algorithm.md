---
title: RSA Algorithm
draft: false
date: 2025-09-22
obsidianUIMode: preview
tags:
  - java
  - Practicals
---
```java

public class RSA{

    public static double GCD(double x, double y){
        double temp;
        while(true){
            temp = x%y;
            if (temp ==0) return y;
            x = y;
            y = temp;
        }
    }
    public static void main(String[] args) {
        double p = 51, q= 53, n =p*q, e=7;
        double fn = (p-1)*(q-1);

        while(e < fn){
            if(GCD(e, fn)==1) break;
            else e++;
        }

        double x = e, y = (1 + (2*fn))/e, msg = 12;

        System.out.println("Ishad Pande, 25, B2");
        System.out.println("------------------");
        System.out.println("RSA Generation Algorithm");
        System.out.print("Prime number are: ");
        System.out.println(p + " and " + q);
        System.out.println("Public Key: " + n);
        
        double i = Math.pow(msg, e) % n;
        System.out.println("Encrypted: " + i);
        System.out.println("Private: " + x);

        double j = Math.pow(i, y) % n;
        System.out.println("Decrypted Data: " + j);
       
    }
}

```
##### Output:
![[Pasted image 20250922233511.png]]