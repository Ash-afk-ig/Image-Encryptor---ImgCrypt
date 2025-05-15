ImgCrypt - Linux Image Encryption Tool
Overview
ImgCrypt is a command-line tool for Linux that provides secure encryption and decryption for image files. It uses AES-256-CBC encryption with PBKDF2 key derivation to ensure your image files remain protected from unauthorized access and tampering.
Features

Strong Encryption: Uses OpenSSL with AES-256-CBC and PBKDF2 for secure encryption
Simple Interface: Easy-to-use command-line interface with color-coded output
Recursive Processing: Option to process entire directories of images
File Backups: Create backups of original files before encryption/decryption
Format Detection: Automatically detects and validates image files
Comprehensive Help: Built-in help and man page support

Installation
Method 1: Automatic Installation

Download both script files (imgcrypt.sh and install.sh)
Make the installer executable:
bashchmod +x install.sh

Run the installer:
bashsudo ./install.sh   # System-wide installation
or
bash./install.sh        # Local user installation


Method 2: Manual Installation

Download the imgcrypt.sh script
Make it executable:
bashchmod +x imgcrypt.sh

Move it to a directory in your PATH:
bashsudo mv imgcrypt.sh /usr/local/bin/imgcrypt   # System-wide installation
or
bashmkdir -p ~/.local/bin
mv imgcrypt.sh ~/.local/bin/imgcrypt          # Local user installation


Usage
Basic Commands
bash# Display help
imgcrypt -h

# Encrypt a single image
imgcrypt -e image.jpg

# Decrypt an encrypted image
imgcrypt -d image.jpg.enc

# Encrypt all images in a directory
imgcrypt -e -r /path/to/images/

# Decrypt all encrypted images in a directory
imgcrypt -d -r /path/to/encrypted/

# Create backups during encryption
imgcrypt -e -b image.jpg
Options

-e, --encrypt: Encrypt image file(s)
-d, --decrypt: Decrypt image file(s)
-r, --recursive: Process directories recursively
-b, --backup: Create backup of original files
-p, --password: Specify password (not recommended, use prompt instead)
-h, --help: Display help message

Supported Image Formats

JPEG (.jpg, .jpeg)
PNG (.png)
BMP (.bmp)
GIF (.gif)
TIFF (.tiff)
WebP (.webp)

Security Notes

ImgCrypt uses industry-standard encryption (AES-256-CBC) with PBKDF2 key derivation
Files are encrypted with a unique salt for each encryption operation
The tool uses 100,000 iterations for PBKDF2 to enhance security
Passwords are never stored or written to disk
For maximum security, avoid using the -p flag and let the tool prompt for passwords instead

Requirements

Bash shell
OpenSSL
File command
Core utilities (basename, dirname, realpath)

License
This tool is provided as free software. Feel free to modify and distribute according to your needs.
Troubleshooting
If you encounter any issues:

Ensure all dependencies are installed:
bashsudo apt-get update && sudo apt-get install openssl file coreutils

Check file permissions for both the tool and target directories
Make sure the password is entered correctly for decryption
For encrypted files that won't decrypt, verify they haven't been corrupted
