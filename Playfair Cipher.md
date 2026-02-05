```java

import java.util.*;

class GfG {

    static void toLowerCase(StringBuilder plain) {
        for (int i = 0; i < plain.length(); i++) {
            if (plain.charAt(i) > 64 && plain.charAt(i) < 91)
                plain.setCharAt(i, (char)(plain.charAt(i) + 32));
        }
    }
    
    static void removeSpaces(StringBuilder plain) {
        StringBuilder temp = new StringBuilder();
        for (int i = 0; i < plain.length(); i++) {
            if (plain.charAt(i) != ' ') {
                temp.append(plain.charAt(i));
            }
        }
        plain.setLength(0);
        plain.append(temp);
    }

    static void generateKeyTable(StringBuilder key, char[][] keyT) {
        int n = key.length();

        int[] hash = new int[26];

        for (int i = 0; i < n; i++) {
            if (key.charAt(i) != 'j')
                hash[key.charAt(i) - 97] = 2;
        }

        hash['j' - 97] = 1;

        int i = 0, j = 0;

        for (int k = 0; k < n; k++) {
            if (hash[key.charAt(k) - 97] == 2) {
                hash[key.charAt(k) - 97] -= 1;
                keyT[i][j++] = key.charAt(k);
                if (j == 5) {
                    i++;
                    j = 0;
                }
            }
        }

        for (int k = 0; k < 26; k++) {
            if (hash[k] == 0) {
                keyT[i][j++] = (char)(k + 97);
                if (j == 5) {
                    i++;
                    j = 0;
                }
            }
        }
    }

    static void search(char[][] keyT, char a, char b, int[] arr) {
        if (a == 'j') a = 'i';
        if (b == 'j') b = 'i';

        for (int i = 0; i < 5; i++) {
            for (int j = 0; j < 5; j++) {
                if (keyT[i][j] == a) {
                    arr[0] = i;
                    arr[1] = j;
                } else if (keyT[i][j] == b) {
                    arr[2] = i;
                    arr[3] = j;
                }
            }
        }
    }

    static int prepare(StringBuilder str) {
        if (str.length() % 2 != 0) {
            str.append('z');
        }
        return str.length();
    }


    static void encrypt(StringBuilder str, char[][] keyT) {
        int[] arr = new int[4];
        for (int i = 0; i < str.length(); i += 2) {
            search(keyT, str.charAt(i), str.charAt(i + 1), arr);

            if (arr[0] == arr[2]) {
                str.setCharAt(i, keyT[arr[0]][(arr[1] + 1) % 5]);
                str.setCharAt(i + 1, keyT[arr[0]][(arr[3] + 1) % 5]);
            } else if (arr[1] == arr[3]) {
                str.setCharAt(i, keyT[(arr[0] + 1) % 5][arr[1]]);
                str.setCharAt(i + 1, keyT[(arr[2] + 1) % 5][arr[1]]);
            } else {
                str.setCharAt(i, keyT[arr[0]][arr[3]]);
                str.setCharAt(i + 1, keyT[arr[2]][arr[1]]);
            }
        }
    }

    static void encryptByPlayfairCipher(
        StringBuilder str, StringBuilder key) {
        char[][] keyT = new char[5][5];
        removeSpaces(key);
        toLowerCase(key);
        toLowerCase(str);
        removeSpaces(str);
        prepare(str);
        generateKeyTable(key, keyT);
        encrypt(str, keyT);
    }

    public static void main(String[] args) {
        StringBuilder key = new StringBuilder("Monarchy");
        StringBuilder str = new StringBuilder("instruments");
        System.out.println("Key text: " + key);
        System.out.println("Plain text: " + str);
        encryptByPlayfairCipher(str, key);
        System.out.println("Cipher text: " + str);
    }
}

```