# Encryption-Key-Strength
Project: Demonstrating Encryption Key Strength
Introduction
This notebook demonstrates the importance of using strong, high-entropy encryption keys and the risks associated with weak keys. It uses the cryptography library in Python to perform symmetric encryption with Fernet, illustrating how a simple 4-digit PIN can be brute-forced relatively quickly, while a randomly generated strong key is computationally infeasible to attack in the same manner.

The notebook covers the following aspects:

Setup and Imports: Installing necessary libraries and importing modules.
Key Derivation: A helper function to derive a Fernet key from a password using PBKDF2HMAC.
File Upload: Allows the user to upload a dataset for encryption.
Weak Key Encryption (Part A): Encrypting data using a 4-digit PIN-derived key.
Brute-Force Attack (Part B): Attempting to brute-force the 4-digit PIN to decrypt the data and measuring the time taken.
Strong Key Encryption (Part C): Encrypting data with a cryptographically strong, randomly generated key.
Insecure Key Storage (Part E): Demonstrating the vulnerability of storing encryption keys alongside encrypted data.
File Downloads (Part F): Providing encrypted and recovered files for download.
Setup and Dependencies
The project uses the cryptography library. This is installed in the first cell of the notebook.

!pip install cryptography --quiet
Other standard libraries like time, os, base64, google.colab.files are also used.

Key Derivation Function
The derive_fernet_key function takes a password (as bytes), a salt, and an optional number of iterations to derive a 32-byte base64-encoded Fernet key using PBKDF2HMAC with SHA256. The number of iterations impacts the strength against brute-force attacks by increasing the computational cost of each guess.

Data Upload
Before running the encryption steps, you will be prompted to upload a CSV file that will be used as the plaintext data for demonstration purposes.

Demonstrations
Part A: Weak Key Encryption
This section encrypts the uploaded file using a key derived from a predefined 4-digit PIN (e.g., "0420"). The key derivation uses a relatively low number of PBKDF2 iterations (kdf_iterations_demo) to simulate a less secure setup, making it susceptible to brute-force.

Output: An encrypted file named encrypted_weak.bin.

Part B: Brute-Force Attack on Weak Key
This part attempts to decrypt the encrypted_weak.bin file by trying every possible 4-digit PIN from "0000" to "9999". It measures the time taken and the number of attempts required to find the correct PIN and recover the original plaintext. This highlights how quickly a weak key can be compromised.

Output: Recovery status, the found PIN, number of attempts, time taken, and a recovered_from_weak.csv file if successful.

Part C: Strong Key Encryption
This section encrypts the original file using a cryptographically strong, randomly generated Fernet key. It emphasizes that such keys, due to their high entropy, are practically immune to brute-force attacks within a reasonable timeframe, even with powerful computing resources.

Output: An encrypted file named encrypted_strong.bin.

Part D & E: Insecure Key Storage
These sections simulate a common security mistake: storing the encryption key (even a weak one) alongside the encrypted data. If an attacker gains access to both, decryption becomes trivial, irrespective of the key's strength.

Output: A file named insecure_key.txt containing the weak key (for demonstration purposes).

Part F: Downloaded Files
This final section allows you to download all the generated files:

encrypted_weak.bin
recovered_from_weak.csv
encrypted_strong.bin
insecure_key.txt
How to Run
Execute All Cells: Simply run all the cells in the notebook sequentially.
Upload CSV: When prompted by cell 4), upload a CSV file (e.g., a small dataset like healthcare_dataset.csv).
Observe Output: Pay attention to the console output for each section, especially the time taken for brute-forcing the weak PIN and the explanations regarding strong keys and insecure storage.
