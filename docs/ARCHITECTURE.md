# Project Citadel: System Architecture

## Table of Contents

- [1. Introduction](#1-introduction)
- [2. High-Level Architecture](#2-high-level-architecture)
  - [2.1. Core Components](#21-core-components)
- [3. Cryptographic Design](#3-cryptographic-design)
  - [3.1. Algorithms](#31-algorithms)
  - [3.2. Key Hierarchy](#32-key-hierarchy)
  - [3.3. Data Flow: Unlocking an Item](#33-data-flow-unlocking-an-item)
- [4. Trust Boundaries](#4-trust-boundaries)
- [5. Data Model and Serialization](#5-data-model-and-serialization)

---

## 1. Introduction

This document provides a detailed overview of the system architecture for Project Citadel. It covers the high-level design, core components, cryptographic architecture, and security principles that guide the project. The primary goal is to create a secure, transparent, and auditable system based on **zero-knowledge** principles.

---

## 2. High-Level Architecture

Project Citadel is designed as a modular, **local-first** system with optional, end-to-end encrypted synchronization. The architecture is composed of three primary layers: a central **Core Library**, various **Client Applications**, and an optional **Sync Server**.

The fundamental design principle is that all cryptographic operations occur on the **client-side**. The server, if used, is treated as an untrusted, zero-knowledge storage provider.

### 2.1. Core Components

* **Vault Core (`vault-core`):** A language-specific library (initially Python, with a planned migration to a performant, portable language like Rust or C++) that contains all business logic for vault management, including all cryptographic operations.
* **Clients:** A suite of applications that consume the `vault-core` library to provide a user interface. This includes:
    * Command-Line Interface (CLI)
    * Desktop GUI (e.g., Tauri)
    * Mobile Apps (iOS/Android)
    * Browser Extension
* **Sync Server:** A stateless, encrypted blob store that facilitates the synchronization of the encrypted vault file across a user's devices.

---

## 3. Cryptographic Design

The security of Project Citadel is built upon a robust and modern cryptographic foundation.

### 3.1. Algorithms

* **Key Derivation Function (KDF):** `Argon2id`. This algorithm was chosen for its strong resistance to both GPU-based and side-channel attacks. KDF parameters (memory, time cost, parallelism) are stored in the vault header to allow for future upgrades.
* **Authenticated Encryption (AEAD):** `XChaCha20-Poly1305`. This provides a high level of security with a large nonce size, which simplifies secure implementation and reduces the risk of nonce reuse. `AES-256-GCM` is a permissible alternative for hardware-accelerated scenarios.
* **Hashing:** `BLAKE3` for fast internal digests and `SHA-256` for interoperability where required.
* **Random Number Generation:** The operating system's Cryptographically Secure Pseudo-Random Number Generator (CSPRNG) is used for generating all keys, salts, and nonces.

### 3.2. Key Hierarchy

The system uses a multi-layered key hierarchy, often called "envelope encryption," to ensure strong data isolation and minimize the exposure of the Master Key.

* **Master Password (MP):** The user's chosen password. This is the only secret the user needs to remember.
* **Master Key (MK):** Derived from the **MP** and a unique salt using `Argon2id`. The **MK** exists only in memory during a session and is never stored on disk.
* **Vault Key (VK):** A randomly generated symmetric key created during vault initialization. The **VK** encrypts all Item Keys. The **VK** itself is encrypted (or "wrapped") by the **MK** and stored within the vault file.
* **Item Key (IK):** A unique, randomly generated symmetric key for each entry in the vault. Each **IK** encrypts the payload of its corresponding item. The **IK** is then encrypted by the **VK**.

### 3.3. Data Flow: Unlocking an Item

The following diagram illustrates the process of decrypting a single item from the vault, demonstrating the key hierarchy in action.

```mermaid
graph TD
    A[User enters Master Password] --> B{Argon2id KDF};
    C[Salt from Vault Header] --> B;
    B --> D[Master Key (MK) in memory];
    E[Encrypted Vault Key (VK_wrapped)] --> F{AEAD Decrypt};
    D --> F;
    F --> G[Vault Key (VK) in memory];
    H[Encrypted Item Key (IK_wrapped)] --> I{AEAD Decrypt};
    G --> I;
    I --> J[Item Key (IK) in memory];
    K[Encrypted Item Payload] --> L{AEAD Decrypt};
    J --> L;
    L --> M[Plaintext Item Data];
```

This flow ensures that the **Master Key** is only used to decrypt a single key (the **VK**), and the **Vault Key** is only used to decrypt the much smaller Item Keys, adhering to the principle of least privilege.

---

## 4. Trust Boundaries

The architecture defines clear trust boundaries to model threats and guide security decisions.

* **Client-Side:** This is the **trusted environment**. All unencrypted data and cryptographic keys (**MK**, **VK**, **IK**) should only ever exist in memory on the client's device. The client is responsible for all encryption and decryption.
* **Server-Side:** This is an **untrusted environment**. The server is designed to be **zero-knowledge**. It stores and transmits encrypted blobs of data but has no access to the keys required to decrypt them. Authentication with the server is designed so the server never handles the user's Master Password (e.g., via a PAKE protocol like OPAQUE).
* **Operating System (OS):** The OS is considered **semi-trusted**. The application relies on the OS for secure random number generation and process isolation. The design aims to mitigate risks where possible (e.g., by zeroizing keys in memory and disabling core dumps). A fully compromised OS (e.g., with a keylogger) is considered out of scope for the initial versions.

---

## 5. Data Model and Serialization

* **Serialization:** The primary serialization format is **CBOR** (Concise Binary Object Representation) for its compactness and extensibility. **JSON** is used as a fallback for debugging and readability.
* **Schema:** A formal schema for the vault and item structures is defined to ensure interoperability and forward compatibility between different client implementations.
* **Metadata Protection:** To prevent information leakage, all sensitive metadata (item titles, usernames, URLs, timestamps) is encrypted within the item payload. Non-sensitive metadata, such as a random UUID for each item, remains in plaintext for synchronization and database indexing purposes.
