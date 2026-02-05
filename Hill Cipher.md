``` java
import java.util.*;

public class p3 {

    // Convert character to integer (A=0, ..., Z=25)
    private static int charToInt(char c) {
        return c - 'A';
    }

    // Convert integer to character
    private static char intToChar(int i) {
        return (char) (i + 'A');
    }

    // Multiply matrix and vector (mod 26)
    private static int[] multiplyMatrix(int[][] key, int[] vec) {
        int[] result = new int[vec.length];
        for (int i = 0; i < key.length; i++) {
            result[i] = 0;
            for (int j = 0; j < key.length; j++) {
                result[i] += key[i][j] * vec[j];
            }
            result[i] %= 26;
        }
        return result;
    }

    // Modular inverse of number a under mod m
    private static int modInverse(int a, int m) {
        a = a % m;
        for (int x = 1; x < m; x++) {
            if ((a * x) % m == 1) return x;
        }
        return -1; // no inverse exists
    }

    // Compute determinant of 3x3 matrix mod 26
    private static int determinant(int[][] m) {
        int det = m[0][0] * (m[1][1]*m[2][2] - m[1][2]*m[2][1])
                - m[0][1] * (m[1][0]*m[2][2] - m[1][2]*m[2][0])
                + m[0][2] * (m[1][0]*m[2][1] - m[1][1]*m[2][0]);
        return (det % 26 + 26) % 26;
    }

    // Get cofactor matrix of 3x3
    private static int[][] cofactorMatrix(int[][] m) {
        int[][] cof = new int[3][3];

        cof[0][0] = (m[1][1]*m[2][2] - m[1][2]*m[2][1]);
        cof[0][1] = -(m[1][0]*m[2][2] - m[1][2]*m[2][0]);
        cof[0][2] = (m[1][0]*m[2][1] - m[1][1]*m[2][0]);

        cof[1][0] = -(m[0][1]*m[2][2] - m[0][2]*m[2][1]);
        cof[1][1] = (m[0][0]*m[2][2] - m[0][2]*m[2][0]);
        cof[1][2] = -(m[0][0]*m[2][1] - m[0][1]*m[2][0]);

        cof[2][0] = (m[0][1]*m[1][2] - m[0][2]*m[1][1]);
        cof[2][1] = -(m[0][0]*m[1][2] - m[0][2]*m[1][0]);
        cof[2][2] = (m[0][0]*m[1][1] - m[0][1]*m[1][0]);

        return cof;
    }

    // Transpose matrix
    private static int[][] transpose(int[][] m) {
        int[][] t = new int[m.length][m.length];
        for (int i = 0; i < m.length; i++) {
            for (int j = 0; j < m.length; j++) {
                t[i][j] = m[j][i];
            }
        }
        return t;
    }

    // Inverse of 3x3 key matrix (mod 26)
    private static int[][] inverseMatrix(int[][] key) {
        int det = determinant(key);
        int invDet = modInverse(det, 26);

        if (invDet == -1) {
            throw new ArithmeticException("Key matrix is not invertible mod 26.");
        }

        int[][] cof = cofactorMatrix(key);
        int[][] adj = transpose(cof);

        int[][] inv = new int[3][3];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                inv[i][j] = (adj[i][j] * invDet) % 26;
                if (inv[i][j] < 0) inv[i][j] += 26;
            }
        }
        return inv;
    }

    // Encryption
    private static String encrypt(String plaintext, int[][] key) {
        plaintext = plaintext.toUpperCase().replaceAll("[^A-Z]", "");
        
        while (plaintext.length() % 3 != 0) {
            plaintext += "X"; // padding
        }

        StringBuilder ciphertext = new StringBuilder();
        for (int i = 0; i < plaintext.length(); i += 3) {
            int[] block = {charToInt(plaintext.charAt(i)), charToInt(plaintext.charAt(i+1)), charToInt(plaintext.charAt(i+2))};
            int[] enc = multiplyMatrix(key, block);
            for (int val : enc) ciphertext.append(intToChar(val));
        }
        return ciphertext.toString();
    }

    // Decryption
    private static String decrypt(String ciphertext, int[][] key) {
        int[][] invKey = inverseMatrix(key);

        StringBuilder plaintext = new StringBuilder();
        for (int i = 0; i < ciphertext.length(); i += 3) {
            int[] block = {charToInt(ciphertext.charAt(i)), charToInt(ciphertext.charAt(i+1)), charToInt(ciphertext.charAt(i+2))};
            int[] dec = multiplyMatrix(invKey, block);
            for (int val : dec) plaintext.append(intToChar(val));
        }
        return plaintext.toString();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Example 3x3 key matrix (must be invertible mod 26)
        int[][] key = {
            {6, 24, 1},
            {13, 16, 10},
            {20, 17, 15}
        };

        System.out.print("Enter plaintext: ");
        String plaintext = sc.nextLine();

        String ciphertext = encrypt(plaintext, key);
        System.out.println("Encrypted: " + ciphertext);

        String decrypted = decrypt(ciphertext, key);
        System.out.println("Decrypted: " + decrypted);

        sc.close();
    }
}

```