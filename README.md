# Recovery Repository

This repository contains encrypted recovery files for dr0's servers.
All files are encrypted — no sensitive information is exposed in plaintext.

## Files

| File | Contents | Passphrase |
|------|----------|------------|
| `passwords.txt.age` | All credentials, SSH key, recovery instructions | A — memorized by owner |
| `home-recovery.tar.gz.age` | HOME docs, break-glass, scripts, threat-response | B — in server.conf AGE_PASSPHRASE_DOCS |
| `zap-recovery.tar.gz.age` | ZAP docs, break-glass, scripts, threat-response | B — in server.conf AGE_PASSPHRASE_DOCS |

## To decrypt documentation and break-glass (Passphrase B)

Install age on any machine:
```bash
sudo apt install age   # Linux
brew install age       # macOS
```

Decrypt:
```bash
age -d home-recovery.tar.gz.age | tar -xzf -
age -d zap-recovery.tar.gz.age | tar -xzf -
```

Passphrase B is stored in `server.conf` as `AGE_PASSPHRASE_DOCS` on both servers.
If servers are unavailable, get Passphrase B from `passwords.txt.age` (see below).

## To decrypt credentials (Passphrase A)
```bash
age -d passwords.txt.age
```

Passphrase A is memorized by the server owner only.
Contact owner or use memorized passphrase.

## Recovery chain if everything is lost

1. Download `passwords.txt.age` from this repo (no login needed — public repo)
2. `age -d passwords.txt.age` → enter Passphrase A (memorized)
3. Get SSH private key + Passphrase B from decrypted file
4. `age -d home-recovery.tar.gz.age | tar -xzf -` → enter Passphrase B
5. Read `break-glass-home.txt` for step-by-step server access and restore
EOFcat > ~/maintenance/recovery/README.md << 'EOF'
# Recovery Repository

This repository contains encrypted recovery files for dr0's servers.
All files are encrypted — no sensitive information is exposed in plaintext.

## Files

| File | Contents | Passphrase |
|------|----------|------------|
| `passwords.txt.age` | All credentials, SSH key, recovery instructions | A — memorized by owner |
| `home-recovery.tar.gz.age` | HOME docs, break-glass, scripts, threat-response | B — in server.conf AGE_PASSPHRASE_DOCS |
| `zap-recovery.tar.gz.age` | ZAP docs, break-glass, scripts, threat-response | B — in server.conf AGE_PASSPHRASE_DOCS |

## To decrypt documentation and break-glass (Passphrase B)

Install age on any machine:
```bash
sudo apt install age   # Linux
brew install age       # macOS
```

Decrypt:
```bash
age -d home-recovery.tar.gz.age | tar -xzf -
age -d zap-recovery.tar.gz.age | tar -xzf -
```

Passphrase B is stored in `server.conf` as `AGE_PASSPHRASE_DOCS` on both servers.
If servers are unavailable, get Passphrase B from `passwords.txt.age` (see below).

## To decrypt credentials (Passphrase A)
```bash
age -d passwords.txt.age
```

Passphrase A is memorized by the server owner only.
Contact owner or use memorized passphrase.

## Recovery chain if everything is lost

1. Download `passwords.txt.age` from this repo (no login needed — public repo)
2. `age -d passwords.txt.age` → enter Passphrase A (memorized)
3. Get SSH private key + Passphrase B from decrypted file
4. `age -d home-recovery.tar.gz.age | tar -xzf -` → enter Passphrase B
5. Read `break-glass-home.txt` for step-by-step server access and restore
