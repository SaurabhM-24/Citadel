Project Citadel: Technical Specifications


Introduction
This document provides the formal technical specifications for Project Citadel. It is intended for developers implementing clients or auditing the project's design. All implementations of Project Citadel MUST adhere to these specifications to ensure interoperability and security.


1. Vault File Format (Version 1)
The Project Citadel vault is a single binary file containing a plaintext header and an encrypted body.

1.1. High-Level StructureThe file is composed of two main parts:
1. Header: A plaintext section containing non-sensitive metadata required to begin the key derivation process.
2. Body: An encrypted payload containing all sensitive vault data. The header is used as the Associated Additional Data (AAD) for the body's AEAD encryption, which cryptographically binds the header to the body.

1.2. Binary Layout
The file follows this binary structure:
Field       Type    Size        Description
magic       bytes   4           Magic number identifying the file type. Must be PMV1.
header_len  u32     4           The length of the header data in bytes (unsigned 32-bit integer, little-endian).
header      bytes   header_len  The vault header, serialized as JSON.
body        bytes   Remainder   The AEAD ciphertext of the VaultData structure.

1.3. Vault Header
The header is a JSON object containing the necessary parameters for key derivation.
Example header (JSON):
{
  "format_version": 1,
  "kdf": "argon2id",
  "kdf_params": {
    "mem": 262144,
    "time": 3,
    "parallel": 4
  },
  "salt": "b64_encoded_salt_here...",
  "vault_id": "uuid_v4_here...",
  "created_at": "ISO_8601_timestamp_here"
}

1.4. Encrypted VaultData
Once the body is decrypted using the Master Key (MK), it reveals the VaultData structure, serialized in CBOR (or JSON for debugging).
VaultData Structure:
{
  "vk_wrapped": bytes,      // The Vault Key (VK), encrypted with the Master Key (MK).
  "items": [ ItemRecord ],  // An array of Item Records.
  "vault_metadata": { ... } // Optional, encrypted metadata about the vault itself.
}

1.5. Item Record
Each ItemRecord within the items array follows this structure.
ItemRecord Structure:
{
  "item_id": "uuid_v4_here",
  "ik_wrapped": bytes,      // The Item Key (IK), encrypted with the Vault Key (VK).
  "payload": bytes,         // The item's data, encrypted with the Item Key (IK).
  "version": 1,
  "created_at": "ISO_8601_timestamp",
  "updated_at": "ISO_8601_timestamp"
}
The decrypted payload contains all sensitive user data, such as title, username, password, url, notes, etc.


2. Sync API Protocol (Version 1)
The optional sync server is a stateless, zero-knowledge encrypted blob store. It never has access to plaintext passwords or vault data.

2.1. Authentication
Authentication MUST be performed using a Password-Authenticated Key Exchange (PAKE) protocol to prevent the server from ever handling the user's Master Password. The recommended protocol is OPAQUE.
- Registration (POST /register): The client and server perform the OPAQUE registration exchange. The server stores a record that allows it to authenticate the user without learning the password.
- Login (POST /login): The client and server perform the OPAQUE login exchange. Upon success, the server returns a short-lived session token (e.g., a JWT) for authenticating subsequent API requests.

2.2. Records API
All API endpoints require a valid session token. The server stores records as opaque, encrypted blobs.
- POST /records/batch: Uploads an array of encrypted records. This endpoint should handle the creation, updating, and deletion of items in a single atomic transaction. Each record in the batch should include its record_id (UUID), the ciphertext, and any non-sensitive metadata required for conflict resolution (e.g., version number, timestamp).
- GET /records?since=<cursor>: Fetches all record changes since the last sync, identified by a server-provided cursor (e.g., a timestamp or transaction ID). This allows for efficient, delta-based syncing.
- POST /devices: Registers a new device's public key, allowing for secure device-to-device communication for features like sync-integrated MFA.
