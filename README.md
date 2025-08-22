Project Citadel: A Zero-Knowledge Password Manager
Project Citadel is a privacy-first, zero-knowledge password manager designed for security, transparency, and user control. It is built on the principle that your data is yours alone and should be accessible only by you.

This project prioritizes a small, auditable core and a clear, documented cryptographic design. It begins as a powerful command-line tool with a roadmap to expand into a full suite of cross-platform applications.


Core Principles
Citadel is built on a foundation of four key principles: 
1. Zero-Knowledge: Your data is encrypted and decrypted entirely on your device. The server (for optional syncing) only ever stores encrypted blobs of data and has no ability to access your master password or your secrets.
2. Local-First: The application works perfectly offline. Your encrypted vault is a file that lives on your device, giving you complete control. Syncing is an optional feature, not a requirement. 
3. Auditable & Transparent: The entire project is open-source. We believe that transparency is essential for trust. The cryptographic design and vault format are clearly documented, allowing for independent review and verification.
4.  Secure by Design: We use modern, peer-reviewed cryptographic algorithms and a robust key hierarchy to protect your data against both online and offline attacks.


Current Status
This project is currently in the alpha stage of development. The primary focus is on stabilizing the core cryptographic library and the Python-based Command-Line Interface (CLI). While the security design is robust, it should be considered experimental until a formal security audit is completed.

Features
- Secure Vault Format: A clearly specified and versioned binary format for your encrypted data.
- Strong Key Derivation: Uses Argon2id to protect your master password against brute-force attacks.
- Modern Encryption: Employs XChaCha20-Poly1305 for authenticated encryption of all vault and item data.
- Per-Item Keys: Each entry in your vault is encrypted with its own unique key, providing better data isolation (envelope encryption).
- Metadata Protection: Critical metadata, such as item titles, URLs, and timestamps, are encrypted to prevent leaking sensitive information.
- Powerful CLI: A full-featured command-line interface for all vault operations.

Planned Features
- Optional E2EE Sync: A zero-knowledge server for syncing your encrypted vault across devices.
- Advanced Multi-Factor Authentication (MFA): Including TOTP and an innovative device-to-device approval system.
- Cross-Platform GUI: Desktop, mobile, and browser extension clients.


Getting Started
(This section will be updated as the project matures)

Currently, the project is available as a Python-based CLI.

Prerequisites:
- Python 3.9+

Installation:
# Clone the repository
git clone https://github.com/your-username/your-repo.git
cd your-repo

# Install dependencies
pip install -r requirements.txt


Basic Usage
Here are a few examples of how to use the citadel CLI.

1. Initialize a new vault:
python citadel.py init --vault ./my_vault.db
# You will be prompted to create a secure master password.

2. Add a new password:
python citadel.py add --vault ./my_vault.db --title "Gmail" --username "user@example.com" --generate
# This will unlock the vault and add a new entry with a securely generated password.

3. List all items in the vault:
python citadel.py list --vault ./my_vault.db

4. Show the details of an entry:
python citadel.py show <item_uuid> --vault ./my_vault.db

5. Copy a password to the clipboard:
(The clipboard will be automatically cleared after 20 seconds)
python citadel.py copy <item_uuid> --field password --vault ./my_vault.db


Roadmap
Our vision for Project Citadel is ambitious. We plan to follow a phased development approach:

Phase 1 (Current):
- Stable Python CLI prototype.
- Fully functional core cryptographic library.
- Comprehensive documentation for architecture and specifications.

Phase 2:
- GUI desktop application (using a cross-platform framework like Tauri).
- Initial sync mechanism (e.g., file-based sync via cloud providers).
- Implementation of TOTP-based MFA.

Phase 3:
- Dedicated zero-knowledge sync server.
- Mobile applications (iOS & Android).
- Browser extension with secure autofill.
- Implementation of device-based MFA.
- Formal third-party security audit.


Contributing
We welcome contributions from the community! Whether it's reporting a bug, suggesting a feature, or submitting code, your help is valued. Please read our CONTRIBUTING.md to get started.

For security-related inquiries or to report a vulnerability, please refer to our SECURITY.md policy.


License
Project Citadel is licensed under the MIT License.
