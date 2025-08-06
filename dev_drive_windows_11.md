# 🛠️ Dev Drive on Windows 11 – Complete Guide

## 📑 Table of Contents

- [✅ What is a Dev Drive?](#-what-is-a-dev-drive)
- [📋 Requirements](#-requirements)
- [🧭 Step-by-Step Setup](#-step-by-step-setup)
  - [1. Open Dev Drive Setup](#1-open-dev-drive-setup)
  - [2. Choose Drive Type](#2-choose-drive-type)
  - [3. Configure Details](#3-configure-details)
- [💻 Optional: Command Line (CLI)](#-optional-command-line-cli)
- [⚠️ Common Errors & Fixes](#-common-errors--fixes)
- [🔄 Removing a Dev Drive](#-removing-a-dev-drive)
- [📈 Why Use a Dev Drive?](#-why-use-a-dev-drive)
- [📌 Summary of Commands](#-summary-of-commands)
- [📚 References](#-references)
- [📚 Appendix: Glossary & Common Questions](#-appendix-glossary--common-questions)


## ✅ What is a Dev Drive?

A **Dev Drive** is a special type of volume in Windows 11 optimized for developers. It:
- Uses the **ReFS file system**
- Enables **Windows Defender Performance Mode** (asynchronous scanning)
- Is ideal for source code, build tools, package managers, etc.

---

## 📋 Requirements

- **Windows 11** version 22H2 (Build 22621.2338 or newer)
- **At least 50 GB of free disk space**
- **8 GB RAM (16 GB recommended)**
- **Administrator privileges**
- Dev Drive may need to be enabled via **Group Policy** or Intune

---

## 🧭 Step-by-Step Setup

### 1. Open Dev Drive Setup
Go to:
**Settings → System → Storage → Advanced storage settings → Disks & volumes → Create Dev Drive**

### 2. Choose Drive Type
- **Create virtual disk (VHD/VHDX)**
- **Shrink existing volume**
- **Use unallocated disk space**

> VHDX (dynamically expanding) is recommended

### 3. Configure Details
- File system: **ReFS** (default)
- Volume size: **≥ 50 GB**
- Drive letter (e.g. `Z:`)
- Dev Drive name

Click **"Create"** to finish setup.

---

## 💻 Optional: Command Line (CLI)

```powershell
# Trust the Dev Drive (important for Defender Performance Mode)
fsutil devdrv trust Z:

# Query trust status
fsutil devdrv query Z:

# Allow specific filters (e.g., Projected File System)
fsutil devdrv setfiltersallowed PrjFlt
```

> ⚠️ You must run PowerShell as **Administrator**

---

## ⚠️ Common Errors & Fixes

| Error | Solution |
|-------|----------|
| Error 5: Access Denied | Run PowerShell as **Administrator** |
| Volume not found | Is `Z:` mounted? Check with `mountvol Z: /L` |
| Not a ReFS volume | Recreate Dev Drive – NTFS is not supported |

---

## 🔄 Removing a Dev Drive

1. Go to **Settings → Storage → Disks & volumes**
2. Select the Dev Drive → **Delete Volume**
3. If VHD-based: Open **Disk Management → Detach VHD**
4. Optionally delete the `.vhdx` file manually

---

## 📈 Why Use a Dev Drive?

- Faster builds and file operations
- Lower Defender scan latency via Performance Mode
- Ideal for development workflows (Node, Git, Go, .NET, etc.)

---

## 📌 Summary of Commands

```powershell
# Trust Dev Drive
fsutil devdrv trust Z:

# Show trust status
fsutil devdrv query Z:

# Allow specific filters
fsutil devdrv setfiltersallowed PrjFlt
```

---

## 📚 References

- [Microsoft Docs – Dev Drive](https://learn.microsoft.com/en-us/windows/dev-drive/)
- [YouTube Tutorial (English)](https://www.youtube.com/watch?v=B83u7l7NFN4)

---

## 📚 Appendix: Glossary & Common Questions

### 🔤 Glossary

| Term | Description |
|------|-------------|
| **Dev Drive** | A developer-optimized storage volume on Windows using ReFS and Defender Performance Mode |
| **ReFS** | Resilient File System – modern file system designed for reliability and scalability |
| **VHD/VHDX** | Virtual Hard Disk formats; VHDX is newer, supports larger volumes, and is more robust |
| **Performance Mode** | Windows Defender mode that reduces real-time scanning latency on trusted Dev Drives |
| **Trusted Drive** | A Dev Drive explicitly marked as trusted by the OS, enabling performance optimizations |
| **fsutil** | Command-line utility for managing file systems and drives on Windows |
| **Projected File System (PrjFlt)** | Windows filter used for technologies like Git Virtual File System (GVFS) |

---

### ❓ Frequently Asked Questions (FAQ)

**Q: What happens if I use NTFS instead of ReFS?**  
A: The Dev Drive won't be optimized. Defender Performance Mode requires ReFS.

**Q: Do I need to recreate my Dev Drive if I move it to another PC?**  
A: Yes, especially if you're using a VHD/VHDX – you’ll need to reattach and trust the volume.

**Q: Can I use Dev Drive for everything?**  
A: No. It's optimized for **source code and development tools**, not general storage or large media files.

**Q: Is it safe to store projects in a Dev Drive?**  
A: Yes – it's built for reliability. Just ensure backups like with any development environment.

**Q: How do I remove a Dev Drive safely?**  
A: Delete it via Settings > Storage. If using a VHDX, detach it in Disk Management, then delete the file.

**Q: Can I create multiple Dev Drives?**  
A: Yes! As long as you have enough free space and system resources.

**Q: How do I verify that Performance Mode is active?**  
A: Use `fsutil devdrv query Z:` to check trust status. If it's trusted, Performance Mode is active.

**Q: Do I need Defender installed?**  
A: Defender must be active for Performance Mode. Third-party antivirus may not support Dev Drive optimizations.

---
