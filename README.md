# DENIC Escrow Key Generator

A standalone, MIT-licensed PHP CLI tool for generating **RFC 9580 OpenPGP v6 keys** for DENIC Registrar Data Escrow (RDE).

## Features

- Ed25519 primary signing key with X25519 encryption subkey
- Passphrase-encrypted private key and configurable expiry
- Securely generated passphrase or an existing protected passphrase file
- ASCII-armored public and private keys, fingerprint metadata, and a pre-signed revoked public certificate
- Restrictive output permissions and key-generation self-checks
- No GnuPG, Sequoia, or external key-generation executables

## Requirements

- PHP 8.3+ with Sodium
- [Composer](https://getcomposer.org/)

## Install and run

```bash
composer install
php escrow_keygen.php
```

The interactive CLI asks for the registrar name, contact email, validity period, output location, and passphrase option. Use `php escrow_keygen.php --help` for details.

Each run creates a protected `denic-keys-*` directory containing `YourPublicKey.asc`, `YourPrivateKey.asc`, `YourPrivateKey.rev.asc`, and `FINGERPRINT.txt`. When a random passphrase is chosen, it also writes `YourPrivateKey.passphrase`.

**Security:** Only share `YourPublicKey.asc` with DENIC. Keep the private key, passphrase, and pre-signed revoked certificate confidential. Store the passphrase separately in a secure vault, then remove the local copy. The revocation file is an already-revoked public certificate; do not submit it unless you intend to revoke the key.

This tool generates keys; it does **not** create or submit escrow deposits.

## License

[MIT](LICENSE). Part of the [Namingo](https://namingo.org/) open-source ecosystem.

Originally extracted from [Namingo Registrar](https://github.com/getnamingo/registrar/blob/main/bin/escrow_keygen.php).
