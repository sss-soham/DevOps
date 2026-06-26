# Week 1 Day 6 - Linux File Permissions & Ownership

Linux is a multi-user system.
Permissions control who can read, write, or execute files.

---

# 🔐 File Permission Basics

Every file has 3 permission types:

r = read  
w = write  
x = execute

They apply to 3 groups:

u = user (owner)  
g = group  
o = others  

---

# 📊 Viewing Permissions

### ls -l

Shows permissions.

Example:
ls -l

Output example:
-rwxr-xr--

Breakdown:
- First character → file type
- Next 3 → owner permissions
- Next 3 → group permissions
- Last 3 → others permissions

---

# 📁 File Type Symbols

- = file  
d = directory  
l = link

Example:
drwxr-xr-x

d = directory

---

# 🔧 chmod (Change Permissions)

Used to modify permissions.

---

## Method 1: Symbolic Mode

Example:
chmod u+x file.sh

Meaning:
Add execute permission to user.

---

More examples:

chmod g-w file.txt  
(Remove write from group)

chmod o+r file.txt  
(Add read to others)

---

## Method 2: Numeric Mode (Important)

Numbers represent:

4 = read  
2 = write  
1 = execute  

Add them:

7 = 4+2+1 (rwx)  
6 = 4+2 (rw-)  
5 = 4+1 (r-x)

---

Example:

chmod 755 file.sh

Meaning:
Owner = rwx (7)  
Group = r-x (5)  
Others = r-x (5)

---

# 👑 chown (Change Owner)

Change file owner.

Example:
sudo chown user file.txt

---

## Change owner + group

sudo chown user:group file.txt

---

Example:
sudo chown soham:devops file.txt

---

# 👥 chgrp (Change Group)

Change group ownership.

Example:
sudo chgrp devops file.txt

---

# 📂 Directory Permissions

Directories use same rwx but meaning differs:

r = list files  
w = create/delete files  
x = enter directory

---

Example:

chmod 755 folder/

Allows:
- Access folder
- Read contents
- Execute inside

---

# 🚀 Real DevOps Examples

### Make script executable

chmod +x deploy.sh

---

### Secure private key

chmod 400 key.pem

---

### Give full access to owner only

chmod 700 private-folder/

---

# 🧠 What I Practiced

- Viewed permissions using ls -l  
- Changed permissions with chmod  
- Changed ownership with chown  
- Understood numeric permission system

---

# 📌 Key Learning

Permissions help in:
- Security
- Access control
- System safety

Wrong permissions can expose system or break apps.
