*This activity has been created as part of the 42 curriculum by salalawn*

## 1. Description
This is the first project in the System and Network module. The goal of this project is to introduce virtualization by creating a virtual server. It focuses on implementing strict security policies, including password complexity, firewall configuration, and managing user permissions to understand how a Linux system is structured and how access is controlled.

## 2. Project Description

### Main Design Choices
* **Partitioning:** I utilized **LVM (Logical Volume Management)** to partition the hard drive. The configuration includes three Logical Volumes (LVs): `root`, `home`, and `swap`.Additionally, there is a separate `/boot` partition that does not belong to the LVM group.
* **Password Policy:** Implemented a strict policy where passwords must be at least 10 characters long, containing uppercase, lowercase, and numbers.Passwords expire every 30 days, must be changed at least 2 days apart, and cannot contain more than 3 consecutive identical characters or the username.

* **Sudo:** Installed and configured `sudo` to avoid direct `root` access.It includes a 3-attempt limit for incorrect passwords, custom error messages, TTY mode enforcement, and full input/output logging in `/var/log/sudo/.

* **User Management:** Created a primary user belonging to the `sudo` and `user42` groups to ensure secure system management without using the root account directly.

* **Services Installed:** Configured **SSH** to run on port **4242** only, with root login strictly forbidden to minimize the attack surface.

* **Firewall:** Enabled **UFW** (Uncomplicated Firewall) to block all incoming traffic except for the specified SSH port (4242).

---

## 3. Technical Comparisons
### Debian vs Rocky Linux
#### Debian
* **Pros:**
    * **Ease of Use:** The `apt` package management system is simple and straightforward.
    * **Stability:** Known as "The Rock" because stable versions are tested for years before release.
    * **Beginner Friendly:** Official advice from 42 School for students new to System Administration.
    * **Lightweight:** Consumes fewer resources (RAM) compared to Rocky.
* **Cons:**
    * **Older Packages:** Focus on stability means software versions are not always the latest.
    * **Less "Enterprise" focused:** Compared to Rocky, large corporations often prefer the Red Hat family.

#### Rocky Linux 
* **Pros:**
    * **Industry Standard:** A binary-compatible clone of Red Hat Enterprise Linux (RHEL), preparing users for major data center environments.
    * **Advanced Security:** Uses SELinux by default, which is a more powerful and complex security system than AppArmor.
    * **Long-term Support:** Backed by major companies for commercial and professional use.
* **Cons:**
    * **Highly Complex:** Difficult configuration that takes time to master (noted as "Complex" in the subject).
    * **Package Management:** Uses `dnf` and `rpm`, which are slightly more intricate than `apt`.
    * **Resource Heavy:** Consumes more system resources than Debian.

### AppArmor vs SELinux
* **AppArmor:** A Path-based Mandatory Access Control (MAC) system. It defines security profiles based on the specific paths of files and programs.
* **SELinux:** A Label-based security system where every process and object has a security label. It is more granular but significantly more complex to manage.

### VirtualBox vs UTM
* **VirtualBox:** A hypervisor designed for x86/amd64 architectures (Intel and AMD). It uses `.vdi` as its primary virtual disk format.
* **UTM:** A hypervisor optimized for Apple Silicon (M1/M2/M3) using ARM architecture. It uses the `.qcow2` format for its disks.

### UFW vs firewalld

Both UFW and firewalld are firewall management tools. Their primary role is to monitor and control incoming and outgoing network traffic based on specific security rules, acting as a barrier to protect the server.

## UFW (Rule-based):

Logic: It treats the server as a "single door" with a global list of rules.

Operation: It works through direct and simple commands; you tell it exactly what to do, like "allow port 4242" or "deny port 80".

Simplicity: It acts more like a script that executes a series of commands. When a rule is changed, it typically requires a quick reload of the entire configuration to apply the new settings.


## firewalld (Zone-based):

Logic: It treats the server as a "group of zones" with varying trust levels.

Operation: Instead of opening ports globally, the rules depend on the environment. For example, you can set a "Public" zone (like at university) to only allow port 4242, while a "Home" zone could allow all traffic.

Dynamism: It runs as a background "Daemon," allowing it to update rules dynamically "on the fly" without interrupting or dropping active user connections. In contrast, UFW might cause a split-second interruption during a reload.
---

## 4. Instructions
* **Installation:** Open VirtualBox and "Import" or "Open" the `.vdi` file.
* **Usage:** Start the machine and log in with the user `salalawn`.
* **SSH Access:** Connect via terminal using: `ssh salalawn@localhost -p 4242`.

## 5. Resources & AI Usage
* **Resources:** 42 Project Subject
* [LVM Guide (Arch Wiki)](https://wiki.archlinux.org/title/LVM)
* [Debian Official Distribution](https://www.debian.org/distrib/)
* [AppArmor Documentation (Ubuntu Wiki)](https://wiki.ubuntu.com/AppArmor#More.2520information)

### AI Usage Description
AI tools were used during this activity for:
* Clarifying system administration concepts like LVM and SSH.
* Drafting and translating technical comparisons for this README.
* Debugging terminal commands during the server setup process.
