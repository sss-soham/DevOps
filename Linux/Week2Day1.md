# Week 2 Day 1 - Linux Networking Commands

Networking knowledge is essential in DevOps for debugging connectivity, servers, and DNS issues.

---

# 🌐 ping

Tests connectivity between your machine and another host.

Example:
ping google.com

What it shows:
- If host reachable
- Response time (latency)
- Packet loss

Stop ping:
CTRL + C

---

# 📡 netstat

Shows network connections, routing tables, and ports.

Examples:
netstat -tuln

Meaning:
t = TCP  
u = UDP  
l = listening ports  
n = numeric output

Useful to check open ports.

---

# 🧾 ifconfig

Displays network interface details.

Example:
ifconfig

Shows:
- IP address
- MAC address
- Network interfaces

Note:
Modern systems use `ip a` instead.

---

# 🛣️ traceroute

Shows path packets take to destination.

Example:
traceroute google.com

Useful to detect:
- Network delays
- Routing issues

---

# 🔍 tracepath

Similar to traceroute but simpler and no sudo needed.

Example:
tracepath google.com

Shows route and MTU info.

---

# 🚀 mtr (My Traceroute)

Combination of ping + traceroute.

Example:
mtr google.com

Shows:
- Real-time packet loss
- Latency per hop

Great for diagnosing network issues.

---

# 🌍 nslookup

Queries DNS to find IP of domain.

Example:
nslookup google.com

Used to debug DNS problems.

---

# 🔌 telnet

Tests connectivity to a specific port.

Example:
telnet google.com 80

Used to check:
- Open ports
- Service availability

Note:
Telnet is old and insecure for login, but useful for testing.

---

# 🧠 What I Practiced

- Tested connectivity using ping
- Checked open ports with netstat
- Viewed IP info using ifconfig
- Traced routes using traceroute
- Debugged DNS with nslookup
- Tested ports using telnet

---

# 🚀 Key Learning

Networking commands help in:
- Server troubleshooting
- DNS debugging
- Connectivity testing
- Monitoring network paths

These are daily-use tools in DevOps.
