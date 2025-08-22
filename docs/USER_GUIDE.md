Project Citadel: User Guide
Welcome to Project Citadel! This guide will walk you through the installation, setup, and basic usage of the Citadel command-line interface (CLI).

1. Installation
Before you begin, make sure you have Python 3.9 or higher installed on your system.
    1. Clone the Repository:
        Open your terminal and run the following command to clone the project from GitHub.
        git clone https://github.com/your-username/citadel.git
        cd citadel

    2. Install Dependencies:
        Install the necessary Python packages using the requirements.txt file.
        pip install -r requirements.txt

You are now ready to use Project Citadel! All commands will be run using python citadel.py.


2. Getting Started: Your First Vault
The first step is to create a secure vault to store your passwords.

Creating a Vault
The init command creates a new, encrypted vault file.
    python citadel.py init --vault ./my_secrets.db

You will be prompted to create and confirm a Master Password.
⚠️ Important Security Note:
Your Master Password is the single key that protects all your data. Choose a strong, unique password that you can remember. If you forget your Master Password, your data will be permanently inaccessible.
After this step, a new file named my_secrets.db will be created. This is your encrypted vault.


3. Core Commands
Here is a reference for the most common commands you will use. For all commands, you'll need to specify the path to your vault file using the --vault flag.

Adding an Entry
Use the add command to store a new password in your vault.
    - Add an entry with a password you choose:
        python citadel.py add --vault ./my_secrets.db --title "Gmail" --username "user@example.com"
        # You will be prompted to enter the password securely.


    - Generate a secure password automatically:
        The --generate flag will create a strong, random password for you.
        python citadel.py add --vault ./my_secrets.db --title "Reddit" --username "my_user" --generate


Listing Entries
The list command shows the titles and unique IDs (item_id) of all entries in your vault.
    python citadel.py list --vault ./my_secrets.db

    Output:
    [item_id] [Title]
    ...
    f7b1c3d4-e5f6-a7b8-c9d0-e1f2a3b4c5d6 Gmail
    a1b2c3d4-e5f6-a7b8-c9d0-e1f2a3b4c5d6 Reddit

Showing an Entry's Details
To view the full details of a specific entry (including the password), use the show command with the entry's item_id.
    python citadel.py show f7b1c3d4-e5f6-a7b8-c9d0-e1f2a3b4c5d6 --vault ./my_secrets.db

Copying a Password to the Clipboard
The copy command securely copies a field (like your password) to the clipboard. For your security, the clipboard will be automatically cleared after 20 seconds.
    python citadel.py copy f7b1c3d4-e5f6-a7b8-c9d0-e1f2a3b4c5d6 --field password --vault ./my_secrets.db

Changing Your Master Password
If you need to change your Master Password, use the change-master command.
    python citadel.py change-master --vault ./my_secrets.db
    # You will be prompted for your old password and then asked to create a new one.


4. Security Best Practices
- Back Up Your Vault: Your vault is a single file (my_secrets.db in our examples). Make sure to create regular backups of this file and store them in a secure location (like an external hard drive). If you lose this file, you lose your data.
- Keep Your Master Password Safe: Do not write down your Master Password or share it with anyone.
- Lock Your Computer: Always lock your computer when you step away to prevent unauthorized access.
