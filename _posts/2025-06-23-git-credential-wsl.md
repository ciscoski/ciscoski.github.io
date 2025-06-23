---
title:  "Using Git Credential Manager (GCM) on Windows inside WSL"
date:   2025-06-23 10:52:00 +0100
categories: wsl2 wsl git 
---

# Using Git Credential Manager (GCM) on Windows inside WSL

This guide shows how to use the Git Credential Manager (GCM) installed on Windows to handle Git credentials securely from within WSL (Windows Subsystem for Linux).

## 🛠️ Prerequisites

- Scoop installed on Windows
- Git Credential Manager installed via Scoop:

```powershell
scoop install git
scoop install git-credential-manager
```

- Git installed in WSL (e.g., Ubuntu):

```bash
sudo apt update
sudo apt install git
```

## 🔗 Configure WSL Git to Use Windows GCM

1. **Create a Git configuration that tells Git in WSL to use the Windows GCM executable**:

```bash
git config --global credential.helper "/mnt/c/Users/<YourUsername>/scoop/shims/git-credential-manager.exe"
```

Replace `<YourUsername>` with your actual Windows username. If unsure, run `cmd.exe /c "echo %USERNAME%"` from WSL.

2. **Set Git to use the correct credential store** (optional, usually auto-detected by GCM):

```bash
git-credential-manager configure
```

3. **Verify GCM is being used**:

```bash
git credential-manager diagnose
```

4. **Test by cloning or pushing to a private repo**:

```bash
git clone https://github.com/your-private/repo.git
```

When prompted, authenticate via the browser or your credential store.

## ✅ Notes

- This setup allows you to share credentials between Windows Git and WSL Git.
- GCM securely stores credentials in the Windows credential manager.
- You can still use SSH for other Git operations if desired.

## 🔐 Troubleshooting

- Ensure WSL has access to the Windows file system (`/mnt/c/...`).
- Make sure GCM is updated with `scoop update git-credential-manager`.
