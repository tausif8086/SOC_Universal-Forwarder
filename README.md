# 🚀 Splunk Enterprise with Universal Forwarder on Ubuntu  
## 🔍 Real-Time Log Monitoring & Centralized Logging

This project demonstrates how to set up **Splunk Enterprise** as a central server and **Universal Forwarder** on Ubuntu to collect system logs like `/var/log/auth.log` in real time. It's perfect for SOC analysts, students, and anyone learning SIEM tools.

---

## 🧰 Tools & Technologies

- 💻 Splunk Enterprise (on Windows/Linux)
- 🐧 Ubuntu 20.04 or 22.04 LTS (Client System)
- 📦 Splunk Universal Forwarder
- 📄 Log Sources: `/var/log/auth.log`, `/var/log/syslog`
- 🔐 UFW (Firewall Configuration - Optional)

---

## ✅ Features

- Centralized and real-time log monitoring
- Easy setup for SIEM practice labs
- Supports Linux authentication log tracking
- Helps detect unauthorized access and sudo usage
- Web-based dashboard for visualization

---

## 🛠 Step-by-Step Setup Guide

### 🔹 Step 1: Install Splunk Enterprise on Server

1. Download from: [https://www.splunk.com/en_us/download/splunk-enterprise.html](https://www.splunk.com/en_us/download/splunk-enterprise.html)  
2. Install it on Windows or Linux  
3. Start Splunk and open: `http://<your-server-ip>:8000`  
4. Set up admin account  
5. Go to **Settings > Indexes** and create a new index: `linux_logs`

---

### 🔹 Step 2: Install Splunk Universal Forwarder on Ubuntu

```bash
# Download Forwarder package
wget -O splunkforwarder.tgz "https://download.splunk.com/products/universalforwarder/releases/9.1.2/linux/splunkforwarder-9.1.2-Linux-x86_64.tgz"

# Extract package
tar -xvzf splunkforwarder.tgz

# Move into Splunk folder
cd splunkforwarder/bin

# Start Splunk Forwarder
sudo ./splunk start --accept-license


🔹 Step 3: Configure the Universal Forwarder

# Enable autostart
sudo ./splunk enable boot-start

# Add Splunk Enterprise server as receiver (replace IP)
sudo ./splunk add forward-server <SPLUNK_SERVER_IP>:9997

# Add Linux log files to monitor
sudo ./splunk add monitor /var/log/auth.log

# Restart to apply
sudo ./splunk restart

🔹 Step 4: Configure Splunk Enterprise to Receive Logs
Go to Settings > Data Inputs > Forwarded Data > Add new TCP

Add TCP port 9997

Assign it to the index linux_logs

Use this Splunk Search to test logs:

index=linux_logs source="/var/log/auth.log"

##🔹 Step 5: Open Firewall Ports (If Needed)

# On Splunk Enterprise server
sudo ufw allow 8000     # Splunk Web UI
sudo ufw allow 9997     # Data receiving port


📊 Use Cases
🔐 Monitor user authentication attempts

🛡️ Detect brute-force SSH attacks

📈 Audit sudo activity and command usage

🧠 Practice SIEM analytics and incident response

🎓 Build cybersecurity lab for SOC training

