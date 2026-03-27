<p align="center">
  <img src="assets/logo.png" alt="FinchBerryOS Logo" width="400">
</p>

# 🫐 FinchBerryOS Frameworks

**FinchBerryOS** is a modern, sovereign operating system based on the Linux kernel, following the architectural philosophy of **macOS/Darwin**. It breaks away from the classic Linux Filesystem Hierarchy Standard (FHS) and introduces a strict, object-oriented bundle structure.



---

## 🏗 Architectural Philosophy

In FinchBerryOS, system resources, libraries, and utilities are not globally scattered. Instead, they are encapsulated within **Framework Bundles (`.frameworkb`)**. This ensures strict encapsulation, version consistency, and a clean system image.

### 📦 GNUCore.frameworkb (The Hardware & Utility Hub)
The `GNUCore.frameworkb` serves as the bridge to the Linux world. It does not contain standard system libraries (like `glibc`), but rather specialized hardware abstractions and system utilities.

* **Hardware & System:** `libudev.so`, `libkmod.so`, `libblkid.so`, `libuuid.so`
* **Graphics & Display:** `libdrm.so`, `libwayland-client.so`, `libwayland-server.so`, `libgbm.so`, `libpixman-1.so`, `libEGL.so`, `libGLESv2.so`
* **Audio & Input:** `libasound.so`, `libinput.so`, `libxkbcommon.so`
* **Utility:** `libffi.so`, `libexpat.so`, `libz.so`
* **Internal Helpers:** Isolated CLI tools for partitioning and filesystem management (e.g., `sgdisk`, `e2fsprogs`, `mkfs.ext4`).

### 🛠 libfinch (The System Bridge)
The central C system library of FinchBerryOS. It links directly against the system `glibc` and provides the APIs required to securely interact with frameworks and their internal helpers.

---

## 📂 Bundle Structure (.frameworkb)

Every framework follows a strict layout to ensure portability and organization:

```text
Name.frameworkb/
├── Name                 # Shared Object / Umbrella Library (.so)
├── Headers/             # C Header files (.h)
├── Contents/
│   ├── Helpers/         # Isolated CLI binaries (disk, fs, network)
│   ├── Resources/       # Assets, icons, localization
│   └── Info.json        # Metadata, versioning & dependencies
