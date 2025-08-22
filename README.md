<div align="center">

  # Project Citadel
  
  **A zero-knowledge, local-first password manager engineered for security, transparency, and user privacy.**
  
</div>

<div align="center">

![Python Version](https://img.shields.io/badge/python-3.9+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-alpha-orange.svg)
![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Core Principles](#core-principles)
- [Project Status](#project-status)
- [Features](#features)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Project Roadmap](#project-roadmap)
- [Contributing](#contributing)
- [Security Policy](#security-policy)
- [License](#license)

## Overview

Project Citadel is an open-source, zero-knowledge password manager designed on the principle of user data sovereignty. It functions as a local-first command-line utility with a development roadmap that includes a full suite of cross-platform applications and an optional, end-to-end encrypted synchronization service.

## Core Principles

The architecture of Citadel is founded on four key principles:

* **Zero-Knowledge:** All cryptographic operations (encryption and decryption) are performed exclusively on the client-side. The synchronization server, if utilized, only stores opaque encrypted blobs and has no access to the master password or the vault's contents.
* **Local-First:** The application is designed to be fully functional offline. The encrypted vault is a local file on the user's device, ensuring complete user control and data ownership.
* **Auditable & Transparent:** As an open-source project, the entire codebase is available for public review. The cryptographic design and vault format specifications are thoroughly documented to facilitate independent analysis and verification.
* **Secure by Design:** The project employs modern, peer-reviewed cryptographic primitives, including Argon2id and XChaCha20-Poly1305, alongside a robust key hierarchy to mitigate a wide range of online and offline attack vectors.

---

## ⚠️ Project Status

This project is currently in the **alpha stage**. The immediate development focus is on stabilizing the core cryptographic library and the Python-based Command-Line Interface (CLI).

> **Disclaimer:** The security design is robust, but the implementation has not yet undergone a formal third-party security audit. Usage in production environments is not recommended at this stage.

---

## Features

### Current Features

* **Secure Vault Format:** A clearly specified and versioned binary format for storing encrypted data.
* **Strong Key Derivation:** Utilizes **Argon2id** for master password hashing to provide significant resistance against brute-force attacks.
* **Authenticated Encryption:** Employs **XChaCha20-Poly1305** for authenticated encryption of all vault and item data, ensuring both confidentiality and integrity.
* **Envelope Encryption:** Each entry within the vault is encrypted with a unique key, providing strong data isolation.
* **Metadata Protection:** Critical metadata, including item titles, URLs, and timestamps, are encrypted to prevent information leakage.
* **Command-Line Interface:** A comprehensive CLI for all vault management operations.

### Planned Features

* Optional End-to-End Encrypted Sync Server
* Multi-Factor Authentication (TOTP, Device-to-Device Approval)
* Cross-Platform GUI Applications (Desktop, Mobile)
* Browser Extension with Secure Autofill Capabilities

---

## Getting Started

### Prerequisites

* Python 3.9+
* Git

### Installation Procedures

1.  **Clone the remote repository:**
    ```sh
    git clone [https://github.com/your-username/your-repo.git](https://github.com/your-username/your-repo.git)
    cd your-repo
    ```

2.  **Install dependencies:**
    It is standard practice to use a virtual environment for dependency management.
    ```sh
    # Create and activate a virtual environment
    python -m venv venv
    source venv/bin/activate  # On Windows, use: venv\Scripts\activate

    # Install required packages from the requirements file
    pip install -r requirements.txt
    ```

---

## Usage

The following examples demonstrate the CLI's functionality.

1.  **Initialize a new vault:**
    Creates a new encrypted vault file and prompts for a master password.
    ```sh
    python citadel.py init --vault ./my_vault.db
    ```

2.  **Add a new entry with a generated password:**
    Adds a new record to the vault and securely generates a password for it.
    ```sh
    python citadel.py add --vault ./my_vault.db --title "Gmail" --username "user@example.com" --generate
    ```

3.  **List all items in the vault:**
    Displays the UUID and title for all entries.
    ```sh
    python citadel.py list --vault ./my_vault.db
    ```

4.  **Show the details of an entry:**
    Provide the item's UUID to retrieve its full details.
    ```sh
    python citadel.py show <item_uuid> --vault ./my_vault.db
    ```

5.  **Copy a password to the clipboard:**
    Copies the password field of the specified entry to the system clipboard. The clipboard is automatically cleared after 20 seconds.
    ```sh
    python citadel.py copy <item_uuid> --field password --vault ./my_vault.db
    ```

---

## Project Roadmap

Development is planned in the following phases:

#### Phase 1 (Current)
- [x] Functional Python CLI prototype
- [x] Core cryptographic library implementation
- [ ] Comprehensive architectural and specification documentation

#### Phase 2
- [ ] Cross-platform GUI desktop application (e.g., Tauri)
- [ ] Initial file-based synchronization mechanism
- [ ] Implementation of TOTP-based MFA

#### Phase 3
- [ ] Dedicated zero-knowledge synchronization server
- [ ] Native mobile applications for iOS and Android
- [ ] Browser extension with secure autofill
- [ ] Device-to-device based MFA
- [ ] Formal third-party security audit

---

## Contributing

Contributions to the project are welcome. Please refer to the **[CONTRIBUTING.md](CONTRIBUTING.md)** file for guidelines on how to submit bug reports, feature requests, and code contributions.

## Security Policy

For information on how to report security vulnerabilities, please see our **[SECURITY.md](SECURITY.md)** policy.

## License

This project is licensed under the terms of the **[MIT License](LICENSE)**.
