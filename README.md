# 🔐 SEED Labs: Symmetric Key Ciphers Lab

This repository contains solutions and reports for the **SEED Labs – Crypto Lab on Symmetric Key Ciphers**, developed using `OpenSSL` and related cryptographic tools.  
The lab involves hands-on practice with encryption algorithms, modes of operation, padding, and secure key usage.

---

## 📁 Contents

```
🔹 Task1_Encryption_Modes/
🔹 Task2_ECB_vs_CBC_Image/
🔹 Task3_Corrupted_Ciphertext/
🔹 Task4_Padding_Schemes/
🔹 Task5_Crypto_Programming/
🔹 screenshots/
🔹 README.md
```

---

## 🧪 Task 1: Encryption using Different Ciphers and Modes

- Used `OpenSSL enc` to test the following combinations:
  - Ciphers: AES-128, AES-192, DES
  - Modes: ECB, CBC, CFB
- Verified encryption/decryption results with custom key and IV values.

### 🔍 Sample Command
```bash
openssl enc -aes-128-cbc -e -in plain.txt -out cipher.bin \
-K 00112233445566778889aabbccddeeff -iv 0102030405060708
```

✅ **Result**: Encrypted and decrypted successfully using multiple combinations.

---

## 🖼️ Task 2: ECB vs CBC Mode – Image Analysis

- Encrypted a `.bmp` file using both ECB and CBC.
- Preserved BMP headers for viewing encrypted files.
- Opened the images in a viewer.

### 🧐 Observations:
- **ECB**: Patterns in the original image were clearly visible in the encrypted version.
- **CBC**: Encrypted image appeared as noise, original content fully obscured.

📌 **Conclusion**: ECB leaks pattern information; CBC provides better confidentiality.

---

## 💥 Task 3: Corrupted Cipher Text

- Encrypted a 64+ byte file using AES-128.
- Flipped a bit in the 30th byte using `ghex`.
- Decrypted using different modes.

### ❓ Pre-analysis (Expectations):

| Mode | Expected Behavior |
|------|-------------------|
| ECB  | Only corrupted block affected |
| CBC  | Corruption propagates to next block |
| CFB  | Bit-flip affects same and next bytes |
| OFB  | Only one byte affected |

### ✅ Result: Confirmed predictions via output comparison.

---

## 🧱 Task 4: Padding

### 🧪 Experiments:
- Encrypted 20-byte and 32-byte files using AES with OpenSSL.
- Observed PKCS#5 padding:
  - 20-byte input: added `0C 0C ...` (12 bytes)
  - 32-byte input (exact multiple): added full block of `10` (16 bytes)
- Compared modes:
  - ECB & CBC → Require padding
  - CFB & OFB → No padding needed (operate as stream ciphers)

📌 **Conclusion**: Padding is necessary for block-based modes when data length ≠ multiple of block size.

---

## 🧑‍💻 Task 5: Programming with OpenSSL EVP

### 📝 Objective:
Brute-force an AES-128-CBC encrypted message using an English dictionary and EVP API.

#### Plaintext:
```
This is a top secret.
```

#### Ciphertext (Hex):
```
8d20e5056a8d24d0462ce74e4904c1b5
13e10d1df4a2ef2ad4540fae1ca0aaf9
```

### ✅ Steps:
- Implemented EVP encryption/decryption in C.
- Appended space characters to words < 16 bytes.
- Iterated over a word list to match ciphertext.

🔑 **Recovered Key**: `Supersecretkey  ` (example)

📌 **Note**: Used `libssl-dev` and linked with `-lcrypto`.

---

## 📸 Screenshots

Screenshots of GHex, encryption results, decrypted outputs, and image analysis are available in the `/screenshots` folder.

---

## 📄 License

This lab is based on the original SEED Lab material developed by Wenliang Du and modified by Mirela Damian.  
Content is shared under the [GNU Free Documentation License 1.2+](http://www.gnu.org/licenses/fdl.html).

---

## ✍️ Author

[Geeta Seshapalli LinkedIn](https://www.linkedin.com/in/your-linkedin-geetaseshapalli)  
Symmetric Key Ciphers Lab Submission | SEED Labs

