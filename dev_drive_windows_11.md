# 🛠️ Dev Drive on Windows 11 – Complete Guide

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
