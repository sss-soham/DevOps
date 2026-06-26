# Week 1 Day 4 - Linux System-Level Commands

## 🖥️ System Information

### uname
Shows system information.

Examples:
uname
uname -a   (all details)

---

### uptime
Shows how long system is running.

Example:
uptime

Displays:
- current time
- uptime
- logged-in users
- load average

---

### date
Shows system date and time.

Example:
date

---

## 👤 User Info Commands

### who
Shows logged-in users.

Example:
who

---

### whoami
Shows current user.

Example:
whoami

---

### id
Shows user ID (UID), group ID (GID).

Example:
id

---

## 🔍 Command Location

### which
Shows path of a command.

Example:
which python
which apt

---

## 🔐 Privilege Management

### sudo
Run commands as superuser.

Example:
sudo apt update

Meaning:
SuperUser DO

---

## 🔄 System Control

### shutdown
Shuts down system.

Examples:
sudo shutdown now
sudo shutdown -h 10  (shutdown in 10 mins)

---

### reboot
Restarts system.

Example:
sudo reboot

---

## 📦 Package Managers

Linux uses different package managers depending on distro.

---

### apt (Debian/Ubuntu)
Used in Ubuntu.

Examples:
sudo apt update
sudo apt upgrade
sudo apt install nginx

---

### yum (RHEL/CentOS)
Used in RedHat-based systems.

Example:
sudo yum install nginx

---

### dnf
New version of yum.

Example:
sudo dnf install nginx

---

### pacman (Arch Linux)
Example:
sudo pacman -S nginx

---

### portage (Gentoo)
Example:
emerge nginx

---

### rpm
Package format used in RHEL-based systems.

Example:
rpm -ivh package.rpm

---

## 🧠 What I Practiced Today
- Learned package managers
- Understood sudo privileges
- Practiced reboot/shutdown commands
---

## 🚀 Key Learning

- Monitoring system health
- Handling user permissions
- Controlling system operations
- Managing software
Linux system commands help in:


