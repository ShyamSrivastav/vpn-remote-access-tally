# vpn-remote-access-tally
Secure remote access infrastructure using OpenVPN, SMB, and Tally Prime

# 🛡️ Remote Access Infrastructure for Tally & SMB over OpenVPN

## 📌 Project Overview

This project showcases the design and deployment of a secure, bidirectional remote access system using **OpenVPN**, **Windows SMB file sharing**, and **Tally Prime license server routing**. The goal was to enable a remote user (my brother) to access my home PC’s shared folders and Tally license server from a different city (200+ km away) over a VPN tunnel, with full authentication, file transfer, and application-level access.

---

## 🧠 Skills Demonstrated

- 🔧 Network architecture & VPN tunneling (OpenVPN TCP)
- 🔐 Windows Firewall configuration & port-based access control
- 🗂️ SMB file sharing with credentialed access
- 🧪 Event Viewer analysis & troubleshooting
- 🧭 Static routing across subnets
- 🧰 Tally Prime license server configuration
- 🧑‍💻 Remote collaboration & real-world testing

---

## 🏗️ Architecture Diagram

![Architechture Diagram](https://github.com/user-attachments/assets/abb92f61-ddda-4a89-9b6c-5996d2a8061c)

---

## 🔧 Key Components

### ✅ VPN Configuration
- Protocol: **TCP** (for reliable file transfer)
- Subnet: `10.8.0.0/24`
- MTU Optimization: `tun-mtu 1400`, `mssfix 1360`
- Static IP assignment for consistent routing

### ✅ SMB File Sharing
- Created a **dedicated Windows user** (`vpnuser`) with read/write access
- Shared folders configured for authenticated access
- Mapped network drives from a remote PC using credentials

### ✅ Tally License Server Access
- Configured `TallyGatewayServer.ini`:
  ```ini
  ServerPort=10000
  ServerBind=0.0.0.0

- Allowed port 10000 in Windows Firewall
- Verified license fetch over VPN (pending final success)

### ✅ Routing & Firewall
Static route added:
- Destination: 192.168.1.0
- Subnet Mask: 255.255.255.0
- Gateway: 10.8.0.14
- Firewall rules scoped to allow traffic from 10.8.0.0/24

---

## 🧪 Troubleshooting Journey
### 🔍 SMB Transfer Failure
- Initial file transfers failed with “socket closed” errors
- Diagnosed short-lived SMB sessions via Event Viewer
    - <!-- Refer to logs from August 30, 2025 between 21:30–21:45 IST  screenshot: Insert Event Viewer log showing SMB logon/logoff -->

### 🔍 Guest Account Limitations
- Identified that Guest account caused premature session termination
- Created vpnuser with full access to resolve

### 🔍 VPN Protocol Optimization
- Switched from UDP to TCP to stabilize large file transfers
- Resulted in successful media file transfer and playback

### 🔍 Routing Failures
- Static route initially misconfigured with subnet as gateway
- Corrected to use 10.8.0.14 (brother’s VPN IP)
- Enabled IP forwarding on remote PC to allow LAN-to-LAN routing

---

## ✅ Current Status
| Component                | Status       | Notes                                                       |
|--------------------------|--------------|-------------------------------------------------------------|
| VPN Tunnel               | ✅ Working   | TCP-based, stable across geographic distance                |
| SMB Access (Mobile)      | ✅ Working   | Successful via mobile file manager with credentials         |
| SMB Access (Remote PC)   | ❌ Pending   | Mapping fails due to Windows credential handling            |
| Tally License Access     | ❌ Pending   | Port 10000 reachable, but license fetch not working         |
| Routing to Remote LAN    | ✅ Working   | Static route + IP forwarding enabled                        |

---

## 📈 What I Learned

- How to design and secure a multi-subnet VPN infrastructure  
- How Windows handles SMB sessions, authentication, and firewall rules  
- How to debug application-level failures using system logs and network traces  
- How to collaborate remotely and simulate enterprise-grade access control  

---

## 🚀 Future Improvements

- Automate VPN IP assignment using `client-config-dir`  
- Resolve SMB access from remote PC via forced credential prompt  
- Finalize Tally license fetch by verifying binding and firewall rules  
- Add monitoring/logging for VPN sessions  
- Extend access to mobile devices with secure SMB clients  

---

## 📂 Repository Structure (Suggested)

<details>
  <summary>📁 Click to expand Repository Structure</summary>

  ```mermaid
    graph TD
    A[vpn-remote-access-tally]
    A --> B[README.md]
    A --> C[configs/]
    C --> C1[server.ovpn]
    C --> C2[client.ovpn]
    C --> C3[TallyGatewayServer.ini]
    A --> D[firewall-rules.md]
    A --> E[troubleshooting-log.md]
    A --> F[screenshots/]
    F --> F1[event-viewer-analysis.png]
    F --> F2[architecture.png]
  ```
</details>

---

## 📸 Screenshot Tags

To make your README visually compelling, consider embedding screenshots at these key points:

- ✅ **Network architecture diagram**  
- ✅ **Event Viewer logs** (Aug 30, 2025, 21:30–21:45 IST)  
- ✅ **Successful SMB access from mobile**  
- ✅ **Static route configuration on router**  
- ✅ **Tally license server config file**  

---

## 🛠️ Status Overview

| Component                | Status       | Notes                                                       |
|--------------------------|--------------|-------------------------------------------------------------|
| VPN Tunnel               | ✅ Working   | TCP-based, stable across geographic distance                |
| SMB Access (Mobile)      | ✅ Working   | Successful via mobile file manager with credentials         |
| SMB Access (Remote PC)   | ❌ Pending   | Mapping fails due to Windows credential handling            |
| Tally License Access     | ❌ Pending   | Port 10000 reachable, but license fetch not working         |
| Routing to Remote LAN    | ✅ Working   | Static route + IP forwarding enabled                        |

---

