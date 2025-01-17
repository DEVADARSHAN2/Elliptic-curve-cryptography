# Ex-11 -Elliptic-curve-cryptography
## AIM:
The implementation of Elliptic Curve Cryptography (ECC) aims to provide strong security with smaller key sizes, enhancing efficiency in encryption, digital signatures, and key exchange.
## ALGORITHM:
STEP-1: Input Parameters
STEP-2: Calculate Public Keys
STEP-3: Display Public Keys
STEP-4: Calculate Shared Secret Keys
STEP-5: Display Shared Secret Keys
STEP-6: Check If Shared Secrets Match
STEP-7: Input the Message to Encrypt
STEP-8: Encrypt the Message
STEP-9: Display the Encrypted Message and the Decrypted Message.
## PROGRAM:
```
#include <stdio.h>

// Function to perform modular addition
int mod_add(int a, int b, int mod) {
    return (a + b) % mod;
}

// Function to perform modular multiplication
int mod_mult(int a, int b, int mod) {
    return (a * b) % mod;
}

// Function to simulate elliptic curve point multiplication (simplified)
int point_multiplication(int G, int private_key, int mod) {
    return mod_mult(G, private_key, mod); // G * private_key % mod
}

int main() {
    int G, nA, nB, p; // Base point G, private keys nA and nB, prime modulus p
    int PA, PB; // Public keys for Alice and Bob
    int KA, KB; // Shared secret keys for Alice and Bob
    int message, encrypted_message, decrypted_message;

    printf("\n ********Elliptic Curve Cryptography(ECC)********\n\n");
    printf("\n NAME: DEVADARSHAN A S REG NO:212222110007\n\n");

    // Get the base point (G) and prime modulus (p) from the user
    printf("Enter the base point (G): ");
    scanf("%d", &G);
    printf("Enter the prime modulus (p): ");
    scanf("%d", &p);

    // Get the private keys for Alice and Bob
    printf("Enter private key for Alice (nA): ");
    scanf("%d", &nA);
    printf("Enter private key for Bob (nB): ");
    scanf("%d", &nB);

    // Calculate the public keys for Alice and Bob
    PA = point_multiplication(G, nA, p); // Alice's public key: PA = nA * G % p
    PB = point_multiplication(G, nB, p); // Bob's public key: PB = nB * G % p
    printf("Alice's public key (PA) = %d\n", PA);
    printf("Bob's public key (PB) = %d\n", PB);

    // Calculate the shared secret keys using the other party's public key
    KA = point_multiplication(PB, nA, p); // Alice's shared secret: KA = nA * PB % p
    KB = point_multiplication(PA, nB, p); // Bob's shared secret: KB = nB * PA % p
    printf("Shared secret calculated by Alice (KA) = %d\n", KA);
    printf("Shared secret calculated by Bob (KB) = %d\n", KB);

    // Both shared secrets should be the same
    if (KA == KB) {
        printf("Success! Both parties have the same shared secret.\n");

        // Get the message to encrypt from the user
        printf("Enter the message to encrypt (as an integer): ");
        scanf("%d", &message);

        // Encrypt the message: ciphertext = (message + shared secret) % p
        encrypted_message = mod_add(message, KA, p);
        printf("Encrypted message: %d\n", encrypted_message);

        // Decrypt the message: plaintext = (ciphertext - shared secret + p) % p
        decrypted_message = (encrypted_message - KA + p) % p;
        printf("Decrypted message: %d\n", decrypted_message);
    } else {
        printf("Error! The shared secrets do not match.\n");
    }

    return 0;
}


```


## OUTPUT:
![Screenshot 2024-10-18 133009](https://github.com/user-attachments/assets/b4c4de1b-8d97-4e7d-b508-d54c9b4164ed)



## RESULT:
Thus the Elliptic curve cryptography (ECC) had been implemented successfully.
