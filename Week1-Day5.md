# Week 1 Day 5 - User & Group Management in Linux

User and group management is important for security and access control in Linux systems.

---

# 🔐 sudo

Run commands with superuser (admin) privileges.

Example:
sudo apt update

Meaning:
SuperUser DO

Used when normal user lacks permission.

---

# 👤 useradd

Create a new user.

Example:
sudo useradd username

Create with home directory:
sudo useradd -m username

Set default shell:
sudo useradd -s /bin/bash username

---

# 🙋 whoami

Shows current logged-in user.

Example:
whoami

---

# 🔄 su

Switch user.

Example:
su username

Switch to root:
su -

Requires password of target user.

---

# 🔑 passwd

Set or change password.

Example:
sudo passwd username

Change own password:
passwd

---

# ❌ userdel

Delete a user.

Example:
sudo userdel username

Delete with home directory:
sudo userdel -r username

---

# 👥 groupadd

Create a new group.

Example:
sudo groupadd devops

---

# ➕ gpasswd

Manage group members.

Add user to group:
sudo gpasswd -a username groupname

Remove user from group:
sudo gpasswd -d username groupname

---

# ❌ groupdel

Delete a group.

Example:
sudo groupdel groupname

---

# 🧠 Why Users & Groups Matter

Linux is multi-user system.

Used for:
- Access control
- Security
- Permission management
- Team collaboration

---

# 🚀 What I Practiced

- Created users and groups
- Set passwords
- Added users to groups
- Switched users
- Deleted users/groups

---

# 📌 Key Learning

Proper user/group management improves:
- System security
- Organization
- Access control


