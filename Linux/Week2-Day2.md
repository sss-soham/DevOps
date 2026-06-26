# Week 2 Day 2 - Advanced Networking & System Commands

These commands are used for network debugging, monitoring, and system-level operations.

---

# 🖥️ hostname

Displays or sets system hostname.

Example:
hostname

Set hostname:
sudo hostname new-name

---

# 🌐 ip

Modern replacement for ifconfig.

Example:
ip a        (show IP address)
ip link     (show interfaces)
ip route    (show routing table)

---

# 🧾 iwconfig

Used for wireless network configuration.

Example:
iwconfig

Shows WiFi details (not used in cloud servers usually).

---

# 🔌 ss

Modern replacement for netstat.

Example:
ss -tuln

Shows:
- Open ports
- Listening services

---

# 📦 arp

Displays ARP table (IP ↔ MAC mapping).

Example:
arp -a

Used in local network troubleshooting.

---

# 🌍 dig

DNS lookup tool (more advanced than nslookup).

Example:
dig google.com

Shows:
- DNS records
- Query time
- Nameserver info

---

# 🔗 nc (netcat)

Networking tool for testing ports & connections.

Example:
nc -zv google.com 80

Used for:
- Port scanning
- Testing services

---

# 🌐 whois

Gets domain registration details.

Example:
whois google.com

Shows:
- Owner info
- Domain expiry

---

# 🔌 ifplugstatus

Checks if network cable is connected.

Example:
ifplugstatus

(Not common in cloud environments)

---

# 🛣️ route

Shows routing table.

Example:
route -n

Tells how traffic is routed.

---

# 🔍 nmap

Network scanner.

Example:
nmap google.com

Used to:
- Scan open ports
- Discover services

---

# 📥 wget

Download files from internet.

Example:
wget https://example.com/file.zip

Supports:
- Resume download
- Background download

---

# ⏱️ watch

Runs command repeatedly.

Example:
watch -n 2 date

Runs every 2 seconds.

Useful for monitoring changes.

---

# 🔥 iptables

Firewall tool in Linux.

Example:
sudo iptables -L

Used for:
- Blocking/allowing traffic
- Security rules

---

# 🛣️ traceroute

Shows path to destination.

Example:
traceroute google.com

Used for debugging network delays.

---

# ⚔️ curl vs wget

### curl
- Used for APIs
- Supports multiple protocols
- Flexible

Example:
curl https://api.github.com

---

### wget
- Used for downloading files
- Simpler than curl

Example:
wget file_url

---

# 🧠 What I Practiced

- Checked IP and routes
- Used ss for port checking
- Performed DNS queries with dig
- Tested ports with netcat
- Downloaded files using wget
- Learned basics of firewall (iptables)

---

# 🚀 Key Learning

Advanced networking tools help in:
- Debugging servers
- Monitoring network traffic
- Securing systems
- Testing APIs and services

Essential for DevOps roles.
