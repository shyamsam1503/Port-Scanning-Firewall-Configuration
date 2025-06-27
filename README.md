# Port-Scanning-Firewall-Configuration
# 

🔐 Project 1: Port Scanning & Firewall Configuration

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Tools](https://img.shields.io/badge/tools-nmap%20%7C%20ufw%20%7C%20kali-blue)
![Red Team vs Blue Team](https://img.shields.io/badge/scenario-Red%20Team%20vs%20Blue%20Team-orange)

> A simulated cybersecurity exercise demonstrating active reconnaissance and firewall configuration using Kali Linux and Ubuntu.

---

## 📘 Overview

This project simulates a **Red Team vs Blue Team** scenario in a controlled virtual lab. The Red Team performs a network scan using Nmap to identify services on a target machine, while the Blue Team hardens the system using the UFW firewall. The goal is to visualize how firewall rules impact visibility and defense.

---

## 🎯 Objectives

- 🔍 Perform reconnaissance using Nmap  
- 🧠 Analyze open/closed/filtered ports  
- 🔐 Configure firewall rules on the target system  
- 🔁 Observe changes before and after hardening  

---

## 🛠️ Lab Setup

| Role     | Operating System | Tooling                 |
|----------|------------------|--------------------------|
| Red Team | Kali Linux       | Nmap for port scanning   |
| Blue Team| Ubuntu Server    | UFW + Services to protect|

📌 Both VMs are connected using **Host-Only Adapter** for internal lab communication.  
🌐 Internet is enabled via **Adapter 1 (NAT)**.

---

## 🔴 Red Team: Attacker Steps

### 1️⃣ Discover Target

```bash
ping 192.168.56.101
```
📌 Purpose: Scans 1000 most common TCP ports of the target. Shows which ports are open.


### 2️⃣ Nmap Scans

```bash
nmap 192.168.56.101
nmap -sV 192.168.56.101
nmap -A -Pn -oN redteam-scan.txt 192.168.56.101
```
📌 Purpose: Performs a more advanced scan to detect which services (and versions) are running on the open ports.

-A: Enables OS detection, version detection, script scanning, and traceroute

-Pn: Disables ping; assumes host is up

-oN: Outputs results to a normal text file (for evidence or documentation)

📝 Output saved in `evidence/redteam-scan.txt`

---

## 🔵 Blue Team: Defender Setup

### 🔧 Service Configuration

#### SSH

```bash
sudo apt update
sudo apt install openssh-server -y
sudo systemctl enable --now ssh
```
📌 Purpose:

openssh-server: Allows remote login via SSH

systemctl: Starts and enables the service so it runs on boot

#### Apache

```bash
sudo apt install apache2 -y
sudo systemctl enable --now apache2
```
📌 Purpose:

Installs Apache2 — opens port 80 (HTTP)

Starts and enables the service

### 🔐 Firewall Configuration

```bash
sudo ufw enable
sudo ufw default deny incoming
sudo ufw allow 22
sudo ufw allow 80    # optional
sudo ufw status verbose
```
📌 Purpose:

Enables firewall and blocks all incoming traffic by default

Only allows necessary ports like:

22 (SSH)

📁 UFW Logs: `evidence/ufw-log.txt`

### 🔄 Verify Changes

```bash
nmap -sV -Pn -oN blueteam-scan.txt 192.168.56.101
```
📌 Purpose:

Checks which ports are visible after firewall hardening

Saves the new scan output to a file

📝 Output saved in `evidence/blueteam-scan.txt`

---

## 🧰 Tools Used

- 🛠️ Nmap  
- 🔥 UFW Firewall  
- 🌐 Apache2  
- 🔐 OpenSSH Server  
- 🧪 Kali Linux & Ubuntu Server  

---

## 📸 Screenshots

Kali Linux

![Image](https://github.com/user-attachments/assets/0fddc87d-ddf8-4534-89f7-03e49dbabfcd)

![Image](https://github.com/user-attachments/assets/84d19e60-a429-4483-b4a1-e94c19100602)

Ubuntu

![Image](https://github.com/user-attachments/assets/9030a07d-ee67-483c-85cd-75175540ff01)

![Image](https://github.com/user-attachments/assets/06ff4d67-660a-44c2-a2dd-448faeb7e153)

---

## 📚 Key Takeaways

- How attackers detect services via open ports  
- The role of firewall rules in threat mitigation  
- Understanding real-world Red Team vs Blue Team dynamics  



