
### 🚀 Powered by ADG System
The original version of this document offers a superior layout and faster navigation. 
**Check it out here:** [Full Documentation Interface](https://draggame-adg-frontend.hf.space/docs/adg_doc_ead162a381aeab081662cb5deae13691)
---

# Project Overview

## **Project Title**  
Seal-Py: A File Ciphering Library  

---

## **Project Goal**  
Seal-Py is a Python-based library designed to provide a simple yet robust solution for encrypting and decrypting text files. The project aims to address the need for secure file ciphering by offering a lightweight and customizable encryption mechanism. This tool is particularly useful for developers and organizations seeking to protect sensitive data in text files without relying on complex or heavyweight encryption frameworks.

---

## **Core Logic & Principles**  
Seal-Py operates on a custom encryption algorithm implemented in the `Enigma` class, which uses a combination of key-based offset manipulation and character substitution. The encryption process involves two main steps:  

1. **Offset Manipulation**:  
   - A numeric offset, derived from the first three characters of the encryption key, is applied to each character in the input text. This shifts the ASCII values of the characters, effectively scrambling them.  

2. **Key-Based Substitution**:  
   - The remaining portion of the key (`keyOf`) is used to further modify the scrambled text. Each character in the text is adjusted based on a calculated key code, which is derived from the position of the character in the text and the length of the key.  

The decryption process reverses these steps, restoring the original text.  

Additionally, the library provides utility methods for generating encryption keys, either randomly or based on a hash input. The keys are tailored to ensure compatibility with the encryption algorithm, maintaining a balance between security and usability.  

The `CipherReader` class extends the functionality by integrating file handling capabilities. It allows users to encrypt or decrypt entire text files, with options to save the output to new files or overwrite the original files.  

The project is implemented in Python (version 3.8 or higher) and adheres to modular programming principles, with separate modules for configuration, utilities, and core encryption logic.  

---

## **Key Features**  
- **Custom Encryption Algorithm**: A lightweight and efficient ciphering mechanism based on offset manipulation and character substitution.  
- **Key Generation**:  
  - Random key generation with customizable length.  
  - Key generation based on hash data for deterministic encryption.  
- **File Encryption and Decryption**:  
  - Encrypt and decrypt text files with ease.  
  - Option to save the output to new files or overwrite existing files.  
- **Utility Methods**: Helper functions for text manipulation and path generation.  
- **Configurable Settings**: A configuration module (`config.py`) for managing encryption-related constants.  

---

## **Dependencies**  
To run Seal-Py, the following dependencies are required:  

1. **Python**: Version 3.8 or higher.  
2. **Poetry**: Used for managing project dependencies and building the library.  

No additional third-party libraries are required, making the project lightweight and easy to integrate into existing Python environments.  

--- 

Seal-Py is a versatile and efficient solution for file encryption, offering a balance between simplicity and security. Its modular design and customizable features make it suitable for a wide range of applications, from personal data protection to enterprise-level file management systems.
## Executive Navigation Tree

### 📄 Core Engine
- [Enigma Class](#enigma-class)
- [Init Method](#init-method)
- [Dependencies](#dependencies)
- [Warnings](#warnings)

### 🔐 Encryption & Decryption
- [Generate Key](#generate-key)
- [Generate Key From Hash](#generate-key-from-hash)
- [Cipher Text](#cipher-text)
- [Anti Cipher Text](#anti-cipher-text)
- [Cipher File](#cipher-file)
- [Anti Cipher File](#anti-cipher-file)
- [Cipher Reader](#cipher-reader)

### 📂 File Management
- [Get Path](#get-path)
<a name="enigma-class"></a> `Enigma` Class: Text Ciphering and Deciphering

The `Enigma` class is a core component responsible for encrypting and decrypting text using a key-based ciphering mechanism. It also provides methods for generating encryption keys based on random values or hash data.

---

####
<a name="init-method"></a> `__init__` Method: Initialization

Initializes the `CipherReader` instance with the file path and reads the file content.

**Inputs, Outputs, and Parameters:**

| Entity       | Type   | Role              | Notes                                                                 |
|--------------|--------|-------------------|-----------------------------------------------------------------------|
| `file_path`  | `str`  | File Path         | Path to the file to be encrypted or decrypted.                       |
| `file`       | `str`  | File Content      | Content of the file read during initialization.                      |

---

####
<a name="dependencies"></a> Dependencies

- **`Enigma` Class:** Provides encryption and decryption methods (`cipher_text` and `anti_cipher_text`) and key generation methods (`generate_key` and `generate_key_from_hash`).  
- **`utilitis` Module:** Provides the `get_text_from_array` function, used to construct file paths from array components.

---

###
<a name="warnings"></a> Critical Notes

1. **Error Handling:** The methods assume valid inputs for file paths and keys. Invalid inputs may cause runtime exceptions.  
2. **File Operations:** Ensure the file paths provided are accessible and writable, especially when `save` or `rewrite` flags are enabled.  
3. **Key Constraints:** The encryption and decryption keys must conform to the format defined by the `Enigma` class.
<a name="generate-key"></a> `generate_key` Method: Key Generation

Generates a random encryption key using the `Enigma` class.

**Inputs, Outputs, and Parameters:**

| Entity       | Type   | Role              | Notes                                                                 |
|--------------|--------|-------------------|-----------------------------------------------------------------------|
| `key_len`    | `int`  | Key Length        | Specifies the length of the generated key. Default is 32.            |
| `key`        | `str`  | Generated Key     | Randomly generated encryption key.                                   |

---

####
<a name="generate-key-from-hash"></a> `generate_key_from_hash` Method: Key Generation from Hash Data

Generates an encryption key based on hash data.

> **Logic:**  
> - Computes a numeric sum of the hash elements.  
> - Adjusts the sum to fall within the range of 200–300.  
> - Constructs the key using the adjusted sum and elements from the hash data.

**Inputs, Outputs, and Parameters:**

| Entity       | Type   | Role              | Notes                                                                 |
|--------------|--------|-------------------|-----------------------------------------------------------------------|
| `hash_data`  | `list` | Hash Data         | List of elements used to compute the key.                            |
| `key`        | `str`  | Generated Key     | Key derived from hash data and adjusted sum.                         |

---

###
<a name="cipher-text"></a> `cipher_text` Method: Text Encryption

Encrypts a given string using the provided key.

> **Logic:**  
> The encryption process involves two steps:  
> 1. **Offset Adjustment:** Each character's ASCII value is incremented by a fixed offset derived from the first three characters of the key.  
> 2. **Key-Based Adjustment:** Each character's ASCII value is further modified based on the remaining part of the key (`keyOf`).  

**Inputs, Outputs, and Parameters:**

| Entity       | Type   | Role              | Notes                                                                 |
|--------------|--------|-------------------|-----------------------------------------------------------------------|
| `text`       | `str`  | Input Text        | The string to be encrypted.                                           |
| `key`        | `str`  | Encryption Key    | Used to calculate the offset and key-based adjustments.               |
| `cipher_text`| `str`  | Encrypted Output  | Resulting encrypted string after applying the ciphering algorithm.    |

---

####
<a name="anti-cipher-text"></a> `anti_cipher_text` Method: Text Decryption

Decrypts a given string using the provided key.

> **Logic:**  
> The decryption process reverses the encryption steps:  
> 1. **Key-Based Adjustment:** Each character's ASCII value is decremented based on the `keyOf` portion of the key.  
> 2. **Offset Adjustment:** Each character's ASCII value is decremented by the fixed offset derived from the first three characters of the key.  

**Inputs, Outputs, and Parameters:**

| Entity           | Type   | Role              | Notes                                                                 |
|------------------|--------|-------------------|-----------------------------------------------------------------------|
| `text`           | `str`  | Encrypted Input   | The string to be decrypted.                                           |
| `key`            | `str`  | Decryption Key    | Used to reverse the offset and key-based adjustments.                 |
| `cipher_text`    | `str`  | Decrypted Output  | Resulting decrypted string after reversing the ciphering algorithm.   |

---

####
<a name="cipher-file"></a> `cipher_file` Method: File Encryption

Encrypts the file content using the provided key and optionally saves the encrypted content to a new file.

> **Logic:**  
> - Uses the `Enigma.cipher_text` method to encrypt the file content.  
> - Determines the save path using the `__get_path` method.  
> - Saves the encrypted content if `save` is `True`.

**Inputs, Outputs, and Parameters:**

| Entity       | Type     | Role              | Notes                                                                 |
|--------------|----------|-------------------|-----------------------------------------------------------------------|
| `key`        | `str`    | Encryption Key    | Key used to encrypt the file content.                                |
| `rewrite`    | `bool`   | Rewrite Flag      | Determines whether to overwrite the original file. Default is `False`.|
| `save`       | `bool`   | Save Flag         | Determines whether to save the encrypted file. Default is `True`.    |
| `cipher_text`| `str`    | Encrypted Content | Resulting encrypted file content.                                    |
| `path`       | `str`    | Save Path         | Path to save the encrypted file.                                     |

---

####
<a name="anti-cipher-file"></a> `anti_cipher_file` Method: File Decryption

Decrypts the file content using the provided key and optionally saves the decrypted content to a new file.

> **Logic:**  
> - Uses the `Enigma.anti_cipher_text` method to decrypt the file content.  
> - Determines the save path using the `__get_path` method.  
> - Saves the decrypted content if `save` is `True`.

**Inputs, Outputs, and Parameters:**

| Entity             | Type     | Role              | Notes                                                                 |
|--------------------|----------|-------------------|-----------------------------------------------------------------------|
| `key`              | `str`    | Decryption Key    | Key used to decrypt the file content.                                |
| `save`             | `bool`   | Save Flag         | Determines whether to save the decrypted file. Default is `True`.    |
| `anti_cipher_text` | `str`    | Decrypted Content | Resulting decrypted file content.                                    |
| `path`             | `str`    | Save Path         | Path to save the decrypted file.                                     |

---

####
<a name="cipher-reader"></a> `CipherReader` Class: File Encryption and Decryption

The `CipherReader` class provides functionality to encrypt and decrypt files using the `Enigma` cipher. It also includes methods for generating encryption keys and managing file paths for saving encrypted and decrypted files.

---

####
<a name="get-path"></a> `__get_path` Method: File Path Management

Generates a new file path with an added suffix and optional endpoint trimming.

> **Logic:**  
> - Splits the original file path into components.  
> - Trims the specified number of endpoints.  
> - Appends the specified suffix to the file name.

**Inputs, Outputs, and Parameters:**

| Entity            | Type     | Role              | Notes                                                                 |
|-------------------|----------|-------------------|-----------------------------------------------------------------------|
| `path`            | `str`    | Original Path     | Path to the original file.                                           |
| `addon_name`      | `str`    | Suffix            | Suffix to append to the file name.                                   |
| `count_endpoints` | `int`    | Endpoint Count    | Number of endpoints to trim from the original path. Default is `1`.  |
| `output_path`     | `str`    | Generated Path    | New file path with the appended suffix.                              |

---

###

    