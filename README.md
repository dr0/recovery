# Recovery Repository

This repository contains encrypted recovery files for dr0's servers.
All files are encrypted — no sensitive information is exposed in plaintext.

## Files

| File | Contents | Passphrase |
|------|----------|------------|
| `passwords.txt.enc` | All credentials, SSH key, recovery instructions | A — memorized by owner |
| `home-recovery.tar.gz.enc` | HOME docs, break-glass, scripts, threat-response | B — in server.conf OPENSSL_DOCS_PASSPHRASE |
| `zap-recovery.tar.gz.enc` | ZAP docs, break-glass, scripts, threat-response | B — in server.conf OPENSSL_DOCS_PASSPHRASE |

## To decrypt documentation and break-glass (Passphrase B)

openssl is pre-installed on Linux and macOS. On Windows use Git Bash.
```bash
openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in home-recovery.tar.gz.enc | tar -xzf -
openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in zap-recovery.tar.gz.enc | tar -xzf -
```

Passphrase B is stored in `server.conf` as `OPENSSL_DOCS_PASSPHRASE` on both servers.
If servers are unavailable, get Passphrase B from `passwords.txt.enc` (see below).

## To decrypt credentials (Passphrase A)
```bash
openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in passwords.txt.enc
```

Passphrase A is memorized by the server owner only.

## Recovery chain if everything is lost

1. Download `passwords.txt.enc` from this repo (no login needed — public repo)
2. `openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in passwords.txt.enc` → enter Passphrase A (memorized)
3. Get Passphrase B from decrypted file
4. `openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in home-recovery.tar.gz.enc | tar -xzf -` → enter Passphrase B
5. Read `break-glass-home.txt` for step-by-step server access and restore
