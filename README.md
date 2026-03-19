# Recovery Repository

This repository contains encrypted recovery files for dr0's servers.
All files are encrypted — no sensitive information is exposed in plaintext.

## Files

| File | Contents | Passphrase |
|------|----------|------------|
| `passwords.txt.enc` | All credentials, SSH key, recovery instructions | Passwords passphrase — memorized by owner |
| `home-recovery.tar.gz.enc` | HOME docs, break-glass, scripts, threat-response | Docs passphrase — in server.conf OPENSSL_DOCS_PASSPHRASE |
| `zap-recovery.tar.gz.enc` | ZAP docs, break-glass, scripts, threat-response | Docs passphrase — in server.conf OPENSSL_DOCS_PASSPHRASE |

## To decrypt documentation and break-glass (Docs passphrase)

openssl is pre-installed on Linux and macOS. On Windows use Git Bash.
```bash
openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in home-recovery.tar.gz.enc | tar -xzf -
openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in zap-recovery.tar.gz.enc | tar -xzf -
```

The docs passphrase is stored in `server.conf` as `OPENSSL_DOCS_PASSPHRASE` on both servers.
If servers are unavailable, get the docs passphrase from `passwords.txt.enc` (see below).

## To decrypt credentials (Passwords passphrase)
```bash
openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in passwords.txt.enc
```

The passwords passphrase is memorized by the server owner only.

## Recovery chain if everything is lost

1. Download `passwords.txt.enc` from this repo (no login needed — public repo)
2. `openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in passwords.txt.enc` → enter passwords passphrase (memorized)
3. Get docs passphrase from decrypted file
4. `openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in home-recovery.tar.gz.enc | tar -xzf -` → enter docs passphrase
5. Read `break-glass-home.txt` for step-by-step server access and restore
