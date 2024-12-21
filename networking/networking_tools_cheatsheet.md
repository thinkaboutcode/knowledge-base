# Network and DNS Tools Cheat Sheet

A collection of popular tools for network and DNS inspection, complete with descriptions, use cases, and availability.

---

## 1. DNS Inspection Tools

### **1.1 dig (Domain Information Groper)**
- **Description**: Command-line tool for querying DNS name servers to retrieve DNS records like A, AAAA, CNAME, MX, and SOA.
- **Use Case**: `dig example.com` to retrieve DNS records for `example.com`.
- **Availability**: Linux, macOS, and Windows (via WSL or third-party install).

### **1.2 nslookup**
- **Description**: Command-line utility to query DNS and obtain information about domain names or IPs.
- **Use Case**: `nslookup example.com` for IP address mappings of `example.com`.
- **Availability**: Default on Windows, Linux, and macOS.

### **1.3 host**
- **Description**: Simple DNS lookup utility for finding IP addresses associated with a domain or its name.
- **Use Case**: `host example.com` shows DNS records.
- **Availability**: Standard on Linux; available for macOS via Homebrew.

### **1.4 WHOIS**
- **Description**: Retrieves domain registration information, including ownership details.
- **Use Case**: `whois example.com` to view registration and ownership details.
- **Availability**: Default on Linux, macOS; installable on Windows.

### **1.5 MXToolbox**
- **Description**: Web-based DNS lookup for MX, A, TXT records, with email server diagnostics.
- **Use Case**: Ideal for troubleshooting email issues, checking MX records.
- **Availability**: Free at [mxtoolbox.com](https://mxtoolbox.com).

---

## 2. Network and Connectivity Tools

### **2.1 ping**
- **Description**: Measures network latency and tests connectivity by sending ICMP echo requests.
- **Use Case**: `ping example.com` to test connectivity to `example.com`.
- **Availability**: Default on Windows, Linux, and macOS.

### **2.2 traceroute (tracert on Windows)**
- **Description**: Shows the path of packets from source to destination, listing each hop and latency.
- **Use Case**: `traceroute example.com` (or `tracert example.com` on Windows) helps diagnose network delays.
- **Availability**: Linux, macOS (`traceroute`); Windows (`tracert`).

### **2.3 ipconfig (Windows) / ifconfig (Linux)**
- **Description**: Displays and manages IP configuration, such as IP, subnet mask, and default gateway.
- **Use Case**: `ipconfig` (Windows) or `ifconfig` (Linux) for network configuration details.
- **Availability**: Default on Windows (`ipconfig`) and Linux (`ifconfig`).

### **2.4 netstat**
- **Description**: Displays active network connections, routing tables, and listening ports.
- **Use Case**: `netstat -a` shows active connections and ports.
- **Availability**: Default on Windows, Linux, and macOS.

### **2.5 Nmap (Network Mapper)**
- **Description**: Network scanning tool for discovering hosts, services, open ports, and OS detection.
- **Use Case**: `nmap -sP 192.168.1.0/24` for scanning a network.
- **Availability**: Linux, macOS, and Windows.

### **2.6 Wireshark**
- **Description**: Packet analyzer for deep inspection of network traffic, capturing and analyzing packets.
- **Use Case**: Network troubleshooting and security analysis.
- **Availability**: Free at [wireshark.org](https://www.wireshark.org/).

### **2.7 curl and wget**
- **Description**: Command-line tools for data transfer, testing HTTP/HTTPS responses.
- **Use Case**: `curl -I example.com` for HTTP headers.
- **Availability**: Most Linux distributions, macOS, and Windows.

### **2.8 OpenSSL**
- **Description**: Toolkit for SSL/TLS protocols, inspecting certificates and secure connections.
- **Use Case**: `openssl s_client -connect example.com:443` to verify SSL certificate.
- **Availability**: Default on Linux, macOS, installable on Windows.

---

## 3. Diagnostic Tools

### **3.1 TCPdump**
- **Description**: Command-line packet analyzer for capturing and displaying network traffic.
- **Use Case**: `tcpdump -i eth0` for capturing packets on `eth0`.
- **Availability**: Default on Linux and macOS; available on Windows as WinDump.

### **3.2 iperf**
- **Description**: Measures network bandwidth between hosts, diagnosing bandwidth issues.
- **Use Case**: `iperf -s` on one host, `iperf -c <server-IP>` on another for bandwidth testing.
- **Availability**: Linux, macOS, and Windows.

### **3.3 Netcat (nc)**
- **Description**: Network utility to read and write data over network connections using TCP/UDP.
- **Use Case**: `nc -l 1234` to open a listener on port `1234`.
- **Availability**: Default on most Linux distributions; available on Windows and macOS.

### **3.4 MTR (My Traceroute)**
- **Description**: Combines `ping` and `traceroute`, showing real-time packet loss and latency.
- **Use Case**: `mtr example.com` for analyzing network performance.
- **Availability**: Linux; installable on macOS and Windows.

---

## 4. Cloud-Based Tools

### **4.1 Google Admin Toolbox (Dig and Ping)**
- **Description**: Web-based suite from Google with `dig`, `ping`, and other DNS/network diagnostics.
- **Use Case**: DNS troubleshooting and testing.
- **Availability**: Free at [Google Admin Toolbox](https://toolbox.googleapps.com/).

### **4.2 DNSChecker.org**
- **Description**: DNS lookup, propagation check, and diagnostics for various record types.
- **Use Case**: Checking DNS propagation across regions.
- **Availability**: Free at [dnschecker.org](https://dnschecker.org).

---

These tools are essential for managing, troubleshooting, and securing networks effectively. Familiarity with each can greatly enhance network analysis and maintenance skills.
