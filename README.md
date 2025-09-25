# EX-8-ADVANCED-ENCRYPTION-STANDARD ALGORITHM
# Aim:
To use Advanced Encryption Standard (AES) Algorithm for a practical application like URL Encryption.

# ALGORITHM:
AES is based on a design principle known as a substitution–permutation.
AES does not use a Feistel network like DES, it uses variant of Rijndael.
It has a fixed block size of 128 bits, and a key size of 128, 192, or 256 bits.
AES operates on a 4 × 4 column-major order array of bytes, termed the state
# PROGRAM:
```
#include <stdio.h> 
#include <math.h> 
int gcd(int a, int b) 
{ 
    while (b != 0)  
    { 
        int temp = b; 
        b = a % b; 
        a = temp; 
    } 
    return a; 
} 
int mod_exp(int base, int exp, int mod)  
{  
    int result = 1; 
    base = base % mod; 
    while (exp > 0) 
    { 
        if (exp % 2 == 1)  
        { 
            result = (result * base) % mod; 
        } 
        exp = exp >> 1; 
        base = (base * base) % mod; 
    } 
    return result; 
} 
 
int mod_inverse(int e, int phi_n)  
{  
    int t = 0, new_t = 1; 
    int r = phi_n, new_r = e; 
    while (new_r != 0)  
    { 
        int quotient = r / new_r; 
        int temp_t = t; 
        t = new_t; 
        new_t = temp_t - quotient * new_t; 
        int temp_r = r; 
        r = new_r; 
        new_r = temp_r - quotient * new_r; 
    } 
    if (r > 1) return -1;  
    if (t < 0) t += phi_n; 
    return t; 
} 
int main()  
{ 
    int p, q, n, phi_n, e, d; 
    int message, encrypted_message, decrypted_message; 
    printf("\n*****Simulation of RSA Encryption and Decryption*****\n\n"); 
    // Get two prime numbers from the user 
    printf("Enter a prime number (p): "); 
    scanf("%d", &p); 
    printf("Enter another prime number (q): "); 
    scanf("%d", &q); 
    n = p * q; 
    phi_n = (p - 1) * (q - 1); 
    do  
    { 
        printf("Enter a value for public key exponent (e) such that 1 < e < %d: ", phi_n); 
        scanf("%d", &e); 
    } while (gcd(e, phi_n) != 1); 
    d = mod_inverse(e, phi_n); 
    if (d == -1)  
    { 
        printf("Modular inverse does not exist for the given 'e'. Exiting.\n"); 
        return 1; 
    } 
    printf("Public key: (n = %d, e = %d)\n", n, e); 
    printf("Private key: (n = %d, d = %d)\n", n, d); 
    printf("Enter the message to encrypt (as an integer): "); 
    scanf("%d", &message); 
    encrypted_message = mod_exp(message, e, n); 
    printf("Encrypted message: %d\n", encrypted_message); 
    decrypted_message = mod_exp(encrypted_message, d, n); 
    printf("Decrypted message: %d\n", decrypted_message); 
    return 0; 
}
```
# OUTPUT:
<img width="1914" height="847" alt="Screenshot 2025-09-25 093949" src="https://github.com/user-attachments/assets/967a868b-28b2-45ce-9ee8-538f975800a8" />

# RESULT:
Thus the program executed successfully.

