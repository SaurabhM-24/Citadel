# Project Citadel: User Guide

This document is the official user guide for the Project Citadel command-line interface (CLI). It provides instructions for installation, initial setup, and command usage.

---

## 1. Installation

**Prerequisite:** A Python 3.9 (or newer) installation is required to run the application.

### 1.1. Clone the Repository
Open a terminal and execute the following commands to clone the project source code and navigate into the project directory.
```bash
git clone [https://github.com/your-username/citadel.git](https://github.com/your-username/citadel.git)
cd citadel
```

### 1.2. Install Dependencies
Install the required Python packages as defined in the `requirements.txt` file.
```bash
pip install -r requirements.txt
```
The installation is now complete. All subsequent operations are performed using the `python citadel.py` script.

---

## 2. Getting Started: Vault Creation

The first step is to initialize a secure vault for data storage.

### 2.1. Initializing a New Vault
The `init` command creates a new, encrypted vault file. The user will be prompted to create and confirm a Master Password during this process.
```bash
python citadel.py init --vault ./my_secrets.db
```
This command generates a new file, `my_secrets.db`, which is the encrypted vault.

> **Security Notice:** The Master Password is the sole credential for accessing vault data. It cannot be recovered. Loss of the Master Password will result in the permanent loss of all data stored within the vault. It is imperative to select a strong, memorable password.

---

## 3. Core Commands

This section provides a reference for the application's core commands. The `--vault` flag, specifying the path to the vault file, is a required argument for all commands listed below.

### 3.1. Add an Entry
The `add` command is used to create a new entry in the vault.

-   **To specify a password manually:**
    The application will prompt for the password to ensure it is not exposed in shell history.
    ```bash
    python citadel.py add --vault ./my_secrets.db --title "Gmail" --username "user@example.com"
    ```

-   **To generate a password automatically:**
    The `--generate` flag creates a cryptographically secure, random password.
    ```bash
    python citadel.py add --vault ./my_secrets.db --title "Reddit" --username "my_user" --generate
    ```

### 3.2. List Entries
The `list` command displays the `item_id` and `title` for all entries in the vault.
```bash
python citadel.py list --vault ./my_secrets.db
```
**Example Output:**
```
[item_id]                              [Title]
------------------------------------   -------
f7b1c3d4-e5f6-a7b8-c9d0-e1f2a3b4c5d6   Gmail
a1b2c3d4-e5f6-a7b8-c9d0-e1f2a3b4c5d6   Reddit
```

### 3.3. Show Entry Details
The `show` command retrieves and displays all data associated with a single entry, identified by its `item_id`.
```bash
python citadel.py show f7b1c3d4-e5f6-a7b8-c9d0-e1f2a3b4c5d6 --vault ./my_secrets.db
```

### 3.4. Copy a Field to the Clipboard
The `copy` command copies the value of a specified field (e.g., `password`) to the system clipboard. The clipboard is automatically cleared after 20 seconds.
```bash
python citadel.py copy f7b1c3d4-e5f6-a7b8-c9d0-e1f2a3b4c5d6 --field password --vault ./my_secrets.db
```

### 3.5. Change Master Password
The `change-master` command facilitates changing the Master Password for the vault. The user will be prompted for the current password and the new password.
```bash
python citadel.py change-master --vault ./my_secrets.db
```

---

## 4. Security Best Practices

-   **Vault Backup**: The vault is a single file (e.g., `my_secrets.db`). Regular backups of this file should be maintained in a secure, offline location. Data loss will occur if this file is lost or corrupted without a backup.
-   **Master Password Security**: The Master Password should be memorized and never written down or stored in any digital format. It should not be shared under any circumstances.
-   **Workstation Security**: Always lock the workstation when it is unattended to prevent unauthorized physical access to an active session.
