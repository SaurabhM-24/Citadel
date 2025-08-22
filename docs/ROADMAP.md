# Project Citadel: Development Roadmap

## Introduction

This document outlines the development roadmap for Project Citadel. Our goal is to build a secure, user-friendly, and trustworthy password manager through a phased, iterative approach.

This roadmap is a living document and may be adjusted based on community feedback, technical challenges, and project priorities.

---

## Phase 1: Foundation (In Progress) 🧱

The primary goal of this phase is to build a robust and secure foundation for the entire project. The focus is on creating a fully functional, local-first command-line tool that can be used as a daily driver.

### Key Milestones

-   [ ] **Core Cryptographic Library:** A stable, well-tested library in Python that handles all encryption, decryption, and key derivation logic.
-   [ ] **Command-Line Interface (CLI):** A feature-complete CLI for all essential vault operations (init, add, show, copy, export, etc.).
-   [ ] **Secure Vault Format v1:** Finalize and document the v1 vault file format specification.
-   [x] **Core Documentation:** Publish initial project documentation, including the `README.md`, `CONTRIBUTING.md`, `SECURITY.md`, and technical specifications.
-   [ ] **Vault Migration Tools:** Develop scripts for importing data from other password managers or standard formats (e.g., CSV).

---

## Phase 2: Desktop & Initial Synchronization 💻

This phase focuses on expanding beyond the CLI to a graphical user interface and introducing the first iteration of cross-device synchronization.

### Key Milestones

-   [ ] **Desktop GUI Application:** A cross-platform desktop application (e.g., using Tauri) that provides a user-friendly graphical interface for managing the vault.
-   [ ] **Initial Sync Mechanism:** Implement a file-based synchronization option, allowing users to sync their encrypted vault file using their own cloud storage provider (e.g., Dropbox, Google Drive, Nextcloud).
-   [ ] **TOTP Multi-Factor Authentication:** Add support for Time-based One-Time Passwords (TOTP) as a second factor for unlocking the vault.
-   [ ] **Hardened Core Library:** Begin porting the core cryptographic library to a language like C++ or Rust for better performance and memory control, ensuring full compatibility with the v1 vault format.

---

## Phase 3: The Ecosystem 🌐

This is the long-term vision for Project Citadel, transforming it into a complete, cross-platform password management ecosystem with a dedicated, secure sync service.

### Key Milestones

-   [ ] **Dedicated Sync Server:** Develop and deploy a zero-knowledge sync server to provide a seamless, real-time synchronization experience across all clients.
-   [ ] **Mobile Applications:** Native mobile apps for both iOS and Android with OS-level integration (e.g., biometric unlock).
-   [ ] **Browser Extension:** A browser extension for major browsers (Chrome, Firefox) with secure, user-initiated autofill capabilities.
-   [ ] **Advanced MFA (Device Approval):** Implement innovative, sync-integrated MFA, allowing users to approve new devices from existing, trusted ones.
-   [ ] **Formal Security Audit:** Engage a reputable third-party firm to conduct a full security audit of the entire ecosystem.
-   [ ] **Team & Shared Vaults:** Introduce features for securely sharing secrets and vaults among family members or teams.

---

We are excited about the future of Project Citadel and look forward to building it with the help of the open-source community.
