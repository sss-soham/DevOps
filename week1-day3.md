# Week 1 Day 3 - Linux Intermediate Commands

## 📝 Text Processing Commands

### wc
Counts lines, words, characters.

Examples:
wc file.txt
wc -l file.txt   (line count)

---

### cut
Extracts columns from text.

Example:
cut -d " " -f1 file.txt

---

### sort
Sorts text alphabetically or numerically.

Example:
sort file.txt

---

### tee
Outputs to screen AND file.

Example:
echo "Hello" | tee file.txt

---

### diff
Shows differences between two files.

Example:
diff file1.txt file2.txt

---

## 🔗 Links in Linux

### Soft Link (Symbolic Link)
Acts like shortcut.

Example:
ln -s original.txt link.txt

---

### Hard Link
Points to same data on disk.

Example:
ln original.txt hardlink.txt

---

## ✍️ vi Editor Basics

Open file:
vi file.txt

Modes:
- Insert mode → press i
- Command mode → press Esc

Save & exit:
:wq

Exit without saving:
:q!

---

## 🔐 Login Related

### ssh
Remote login to servers.

Example:
ssh user@server-ip

---

## 💾 Disk Usage

### df
Shows disk space usage.

Example:
df -h

---

### du
Shows directory size.

Example:
du -sh foldername

---

## ⚙️ Process Commands

### ps
Shows running processes.

Example:
ps aux

---

### top
Live process monitor.

Example:
top

Press q to exit.

---

### kill
Stops a process.

Example:
kill PID

---

### fuser
Shows which process uses a file/port.

Example:
fuser 80/tcp

---

### nohup
Run process in background.

Example:
nohup command &

---

### free
Shows memory usage.

Example:
free -h

---

## 🧹 clear
Clears terminal.

Example:
clear

---

## 🧠 What I Practiced Today

- Text processing commands
- File linking
- Process monitoring
- Disk usage checks
- vi editor basics
- SSH login usage

---

## 🚀 Key Learning

Linux provides powerful tools for:
- Text processing
- Process management
- Disk monitoring
- Remote access

Understanding these is essential for DevOps.
