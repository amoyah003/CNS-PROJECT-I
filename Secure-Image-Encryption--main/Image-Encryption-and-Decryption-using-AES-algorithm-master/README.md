# Image Encryption and Decryption using AES Algorithm

## Overview
This Python-based application provides robust encryption and decryption capabilities for image files. By leveraging advanced cryptographic techniques, it safeguards sensitive visual data from unauthorized access and potential breaches.

## Features
- **Strong Encryption:** Employs AES encryption to ensure data confidentiality.
- **Efficient Performance:** Optimized encryption and decryption processes for fast execution.
- **User-Friendly Interface:** Intuitive GUI simplifies operations for users of all levels.

## System Requirements
- **Operating System:** Ubuntu 18.04.2 (recommended) or later
- **Python:** Version 3.x recommended
- **Libraries:** numpy, Pillow, pycryptodome, Tkinter

## Installation
### Step 1: Install Dependencies
```bash
sudo apt-get install python3-tk
pip install numpy Pillow pycryptodome
```

### Step 2: Download the Tool
Clone the repository or download the source code and extract it to your desired location.

```bash
git clone https://github.com/your-repo/Image-Encryption.git
cd Image-Encryption
```

## Usage
### Encryption Process
1. Launch the application:
   ```bash
   python image_encryption.py
   ```
2. Select the input image file.
3. Enter a strong encryption key.
4. Specify the output file path.
5. Click the **Encrypt** button.

#### Encryption Code 
```python
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
import hashlib
from PIL import Image
import numpy as np
import binascii

def encrypt(image_path, password):
    password = hashlib.sha256(password.encode()).digest()
    image = Image.open(image_path)
    width, height = image.size
    pixels = np.array(image)
    
    pixel_bytes = pixels.tobytes()
    padded_bytes = pad(pixel_bytes, AES.block_size)
    cipher = AES.new(password, AES.MODE_CBC, b'This is an IV456')
    encrypted_bytes = cipher.encrypt(padded_bytes)
    
    with open(image_path + ".crypt", 'wb') as encrypted_file:
        encrypted_file.write(encrypted_bytes)
    
    print("Encryption successful!")
```

### Decryption Process
1. Launch the application:
   ```bash
   python image_encryption.py
   ```
2. Select the encrypted image file.
3. Enter the correct encryption key.
4. Specify the output file path.
5. Click the **Decrypt** button.

#### Decryption Code 
```python
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad

def decrypt(encrypted_path, password):
    password = hashlib.sha256(password.encode()).digest()
    
    with open(encrypted_path, 'rb') as encrypted_file:
        encrypted_bytes = encrypted_file.read()
    
    cipher = AES.new(password, AES.MODE_CBC, b'This is an IV456')
    decrypted_bytes = unpad(cipher.decrypt(encrypted_bytes), AES.block_size)
    
    with open("decrypted_image.jpg", 'wb') as decrypted_file:
        decrypted_file.write(decrypted_bytes)
    
    print("Decryption successful!")
```

## Security Considerations
- Choose a strong and unique encryption key.
- Do not share the encryption key with unauthorized individuals.
- Store encrypted image files securely.

## Limitations
- Currently supports only image files in formats like JPEG, PNG.
- Encryption strength depends on the security of the provided key.

## Disclaimer
This tool provides high-level security, but additional security measures should be considered for comprehensive data protection.

**Note:** For best performance and compatibility, use the recommended system configuration.

## Contact
For inquiries and support, contact: **tonyamoyah3@gmail.com**

