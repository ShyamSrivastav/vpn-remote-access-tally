# 🔐 Firewall Rules for VPN + SMB + Tally Access

This document outlines the firewall rules configured on the host PC to enable secure and uninterrupted access to shared folders and the Tally license server over OpenVPN.

---

## ✅ Inbound Rules

### 1. OpenVPN (TCP Port 1194)
- **Protocol**: TCP  
- **Port**: 1194  
- **Scope**: Allow from `10.8.0.0/24`  
- **Profile**: Private  
- **Action**: Allow

### 2. SMB File Sharing (TCP Port 445)
- **Protocol**: TCP  
- **Port**: 445  
- **Scope**: Allow from `10.8.0.0/24` and `192.168.1.0/24`  
- **Profile**: Private  
- **Action**: Allow

### 3. Tally License Server (TCP Port 10000)
- **Protocol**: TCP  
- **Port**: 10000  
- **Scope**: Allow from `10.8.0.0/24` and `192.168.1.0/24`  
- **Profile**: Private  
- **Action**: Allow

### 4. ICMP (Ping)
- **Protocol**: ICMPv4  
- **Type**: Echo Request  
- **Scope**: Allow from `10.8.0.0/24` and `192.168.1.0/24`  
- **Profile**: Private  
- **Action**: Allow

---

## 🔧 Notes

- All rules were created using **Windows Defender Firewall → Advanced Settings**
- Rules apply only to **Private network profile** to avoid exposure on public networks
- Tally license server must be bound to `0.0.0.0` to accept remote connections

<!-- screenshot: Insert screenshot of firewall rule configuration here -->
