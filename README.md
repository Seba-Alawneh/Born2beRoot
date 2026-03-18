# 🖥️ 42 System & Network Project

> This activity has been created as part of the 42 curriculum by **salalawn**

---

## 📌 1. Description
This is the first project in the System and Network module. The goal of this project is to introduce virtualization by creating a virtual server.  

It focuses on implementing strict security policies, including:
- Password complexity  
- Firewall configuration  
- Managing user permissions  

The objective is to understand how a Linux system is structured and how access is controlled.

---

## ⚙️ 2. Project Description

### 🧩 Main Design Choices

#### 💽 Partitioning
- Utilized **LVM (Logical Volume Management)** to partition the hard drive.  
- Configuration includes three Logical Volumes (LVs):
  - `root`
  - `home`
  - `swap`
- A separate `/boot` partition exists outside the LVM group.

---

#### 🔐 Password Policy
- Minimum length: **10 characters**
- Must include:
  - Uppercase letters
  - Lowercase letters
  - Numbers
- Additional rules:
  - Expire every **30 days**
  - Must be changed at least **2 days apart**
  - Cannot contain:
    - More than **3 consecutive identical characters**
    - The **username**

---

#### 🛡️ Sudo Configuration
- Installed and configured `sudo` to avoid direct root access.
- Features:
  - 3-attempt limit for incorrect passwords
  - Custom error messages
  - TTY mode enforcement
  - Full input/output logging in:
    ```
    /var/log/sudo/
    ```

---

#### 👤 User Management
- Created a primary user belonging to:
  - `sudo` group
  - `user42` group  
- Ensures secure system management without using root directly.

---

#### 🌐 Services Installed
- Configured **SSH**:
  - Runs on port `4242`
  - Root login **disabled**

---

#### 🔥 Firewall
- Enabled **UFW (Uncomplicated Firewall)**
- Rules:
  - Block all incoming traffic
  - Allow only SSH on port `4242`

---

## ⚖️ 3. Technical Comparisons

### 🐧 Debian vs Rocky Linux

#### Debian

**Pros:**
- Easy to use (`apt` package manager)
- Very stable ("The Rock")
- Beginner-friendly (recommended by 42)
- Lightweight (low RAM usage)

**Cons:**
- Older package versions
- Less enterprise-focused

---

#### Rocky Linux

**Pros:**
- Industry standard (RHEL-compatible)
- Advanced security (SELinux)
- Long-term support

**Cons:**
- Complex configuration
- Uses `dnf` and `rpm` (more complex than apt)
- Higher resource usage

---

### 🔒 AppArmor vs SELinux

**AppArmor**
- Path-based MAC system
- Security rules based on file/program paths

**SELinux**
- Label-based system
- More granular and powerful
- More complex to manage

---

### 💻 VirtualBox vs UTM

**VirtualBox**
- Designed for x86/amd64 (Intel & AMD)
- Uses `.vdi` format

**UTM**
- Optimized for Apple Silicon (ARM)
- Uses `.qcow2` format

---

### 🔥 UFW vs firewalld

#### UFW (Rule-based)

- **Logic:** Single door with global rules  
- **Operation:** Direct commands  
  - Example:
    ```
    allow port 4242
    deny port 80
    ```
- **Simplicity:** Easy and script-like  
- **Note:** Requires reload to apply changes

---

#### firewalld (Zone-based)

- **Logic:** Multiple zones with trust levels  
- **Operation:** Rules depend on environment  
  - Example:
    - Public zone → allow 4242 only
    - Home zone → allow more access
- **Dynamism:** Updates rules without interrupting connections  
- Runs as a background daemon

---

## 🚀 4. Instructions

### Installation
- Open VirtualBox  
- Import or open the `.vdi` file  

### Usage
- Start the machine  
- Log in using:
  ```
  salalawn
  ```

### SSH Access
```
ssh salalawn@localhost -p 4242
```

---

## 📚 5. Resources & AI Usage

### Resources
- [42 Project Subject](https://cdn.intra.42.fr/pdf/pdf/135156/en.subject.pdf)
- [LVM Guide (Arch Wiki)](https://wiki.archlinux.org/title/LVM)
- [Debian Official Distribution](https://www.debian.org/distrib/)
- [AppArmor Documentation (Ubuntu Wiki)](https://wiki.ubuntu.com/AppArmor)

---

### AI Usage Description
AI tools were used during this activity for:

- Clarifying system administration concepts like LVM and SSH  
- Drafting and translating technical comparisons for this README  
- Debugging terminal commands during the server setup process  
