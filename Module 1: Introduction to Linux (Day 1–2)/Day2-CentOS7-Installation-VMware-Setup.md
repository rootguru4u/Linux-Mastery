# Day 2: CentOS 7 Installation & VMware Lab Setup

---
**📚 Course:** rootguru Linux Classes  
**🌐 Website:** [www.rootguru.info](http://www.rootguru.info)  
**📖 Document:** Linux Fundamentals - Day 2 Installation & Setup Guide  
**🎯 Level:** Absolute Beginner  
**⏱️ Duration:** 4-5 hours  
**💻 Platform:** CentOS 7 on VMware Workstation Pro 17  
**👨‍🏫 Created by:** rootguru Team  

---

## 📖 Table of Contents

1. [Lab Environment Overview](#lab-environment-overview)
2. [VMware Workstation Pro 17 Setup](#vmware-workstation-pro-17-setup)
3. [Downloading CentOS 7 ISO](#downloading-centos-7-iso)
4. [Creating Virtual Machine](#creating-virtual-machine)
5. [CentOS 7 Installation Process](#centos-7-installation-process)
6. [Understanding Linux Partitioning](#understanding-linux-partitioning)
7. [Manual Partitioning Setup](#manual-partitioning-setup)
8. [Network Configuration](#network-configuration)
9. [Initial System Configuration](#initial-system-configuration)
10. [Post-Installation Tasks](#post-installation-tasks)
11. [VMware Tools Installation](#vmware-tools-installation)
12. [Network Troubleshooting](#network-troubleshooting)
13. [Creating Multiple VMs for Practice](#creating-multiple-vms-for-practice)
14. [Best Practices and Tips](#best-practices-and-tips)
15. [Practice Exercises](#practice-exercises)

---

## 🏢 Lab Environment Overview

### **Professional Lab Setup Architecture**

#### **Enterprise-Grade Virtual Lab Design**
```
┌─────────────────────────────────────────────────────────────────┐
│                  rootguru Linux Lab Environment                 │
└─────────────────────────────────────────────────────────────────┘

Physical Host System:
┌─────────────────────────────────────────────────────────────────┐
│                    Windows/Mac Host Computer                   │
│                                                                 │
│ • Minimum 8GB RAM (16GB recommended)                          │
│ • 100GB free disk space                                       │
│ • Intel VT-x/AMD-V virtualization enabled                     │
│ • VMware Workstation Pro 17 installed                         │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                VMware Virtual Network Architecture              │
│                                                                 │
│ Virtual Network: VMnet8 (NAT) - 192.168.xxx.0/24             │
│                                                                 │
│ ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐ │
│ │   CentOS7-VM1   │  │   CentOS7-VM2   │  │   CentOS7-VM3   │ │
│ │                 │  │                 │  │                 │ │
│ │ • 2GB RAM       │  │ • 1GB RAM       │  │ • 1GB RAM       │ │
│ │ • 20GB Disk     │  │ • 15GB Disk     │  │ • 15GB Disk     │ │
│ │ • Server Role   │  │ • Client Role   │  │ • Test Role     │ │
│ │ • Full Install  │  │ • Minimal       │  │ • Desktop       │ │
│ └─────────────────┘  └─────────────────┘  └─────────────────┘ │
└─────────────────────────────────────────────────────────────────┘

Lab Benefits:
✅ Safe isolated environment
✅ Snapshot and rollback capability  
✅ Multiple OS testing
✅ Network simulation
✅ Real-world server experience
✅ No risk to host system
```

#### **Hardware Requirements and Recommendations**
```
Minimum System Requirements:
┌─────────────────────────────────────────────────────────────────┐
│ Component      │ Minimum      │ Recommended  │ Professional     │
├────────────────┼──────────────┼──────────────┼──────────────────┤
│ RAM            │ 8GB          │ 16GB         │ 32GB+            │
│ CPU            │ Dual Core    │ Quad Core    │ 8+ Cores         │
│ Storage        │ 100GB free   │ 250GB SSD    │ 500GB+ NVMe      │
│ Virtualization │ VT-x/AMD-V   │ VT-x/AMD-V   │ VT-d/IOMMU       │
│ Network        │ Ethernet     │ Gigabit      │ Multiple NICs    │
└────────────────┴──────────────┴──────────────┴──────────────────┘

Performance Optimization:
• Enable hardware virtualization in BIOS
• Allocate adequate RAM to VMs
• Use SSD storage for better I/O performance
• Close unnecessary host applications
• Consider dedicated lab machine for serious learning
```

---

## 🖥️ VMware Workstation Pro 17 Setup

#### **Initial VMware Configuration**
```
Essential VMware Settings Configuration:

🛠️ Global Preferences Setup:
File → Preferences → General:
┌─────────────────────────────────────────────────────────────────┐
│ Default location for VMs: D:\Virtual Machines (or SSD drive)   │
│ Virtual machine directory: Keep organized by project           │
│ Recent VM list: 10 (convenient for quick access)               │
│ Check for updates: Weekly (stay current)                       │
└─────────────────────────────────────────────────────────────────┘

🛠️ Memory Settings:
Edit → Preferences → Memory:
┌─────────────────────────────────────────────────────────────────┐
│ Reserve all guest memory: ✅ (better performance)              │
│ Additional memory: Allow some host memory swap                 │
│ Maximum recommended: 75% of host RAM                          │
└─────────────────────────────────────────────────────────────────┘

🛠️ Network Configuration:
Edit → Virtual Network Editor:
┌─────────────────────────────────────────────────────────────────┐
│ VMnet0 (Bridged): Direct connection to physical network        │
│ VMnet1 (Host-only): Isolated network for VMs and host         │
│ VMnet8 (NAT): VMs share host's IP, internet access            │
│                                                                 │
│ For CentOS lab: Use VMnet8 (NAT) - provides internet access   │
│ Subnet: 192.168.xxx.0/24 (varies by installation)            │
│ DHCP: Enabled (automatic IP assignment)                       │
└─────────────────────────────────────────────────────────────────┘
```

#### **Performance Optimization**
```bash
# Host System Optimization for VMware:

# Windows Host Optimization:
# 1. Disable unnecessary startup programs
msconfig
# Services tab → Hide all Microsoft services → Disable non-essential

# 2. Set Windows for best performance:
# System Properties → Advanced → Performance → Settings
# "Adjust for best performance" or "Custom" with minimal visual effects

# 3. Increase virtual memory:
# System Properties → Advanced → Virtual Memory
# Set initial and maximum size to same value (1.5x physical RAM)

# 4. Power settings:
# Control Panel → Power Options → High Performance

# VMware-specific optimizations:
# 1. Allocate adequate but not excessive RAM to VMs
# 2. Use VMDK files on SSD if available
# 3. Enable hardware acceleration
# 4. Close unnecessary host applications during VM use
```

---

## 💿 Downloading CentOS 7 ISO

### **Obtaining CentOS 7 Installation Media**

#### **CentOS 7 Download Sources and Selection**
```
┌─────────────────────────────────────────────────────────────────┐
│                    CentOS 7 Download Guide                     │
└─────────────────────────────────────────────────────────────────┘

🌐 Official Download Sources:
1. Main Site: centos.org/download/
2. Mirror List: mirror.centos.org/centos/7/isos/x86_64/
3. Direct Links: vault.centos.org (archived versions)

📦 CentOS 7 ISO Variants:
┌─────────────────────────────────────────────────────────────────┐
│ ISO Type              │ Size    │ Description               │ Use │
├───────────────────────┼─────────┼───────────────────────────┼─────┤
│ DVD ISO               │ ~4.5GB  │ Complete installation    │ ⭐   │
│ Everything ISO        │ ~8.5GB  │ All packages included    │ Pro │
│ Minimal ISO           │ ~900MB  │ Command line only        │ Srv │
│ NetInstall ISO        │ ~500MB  │ Network-based install    │ Adv │
└───────────────────────┴─────────┴───────────────────────────┴─────┘

🎯 Recommended for Beginners: CentOS-7-x86_64-DVD-2009.iso
   • Complete package set
   • GUI and command line options
   • No internet required during installation
   • Good for learning all features
```

#### **Download Process and Verification**
```bash
# Recommended download method:

# 1. Choose fastest mirror near your location:
# Visit: mirror.centos.org/centos/7/isos/x86_64/

# 2. Download files needed:
CentOS-7-x86_64-DVD-2009.iso           # Main installation file
sha256sum.txt                          # Checksum verification file

# 3. Verify download integrity (Windows):
# Download HashTab or use PowerShell:
Get-FileHash -Algorithm SHA256 "CentOS-7-x86_64-DVD-2009.iso"

# Compare with published checksum from sha256sum.txt:
# 659691c28a4e8c6632aebf8a7409e63a3a3c52dd7e9b9c9e8a7a8c5b5f5a5b5a

# 4. Alternative download using wget (Linux/macOS):
wget http://vault.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-2009.iso

# 5. Verify checksum (Linux/macOS):
sha256sum CentOS-7-x86_64-DVD-2009.iso
```

---

## 🖥️ Creating Virtual Machine

### **Setting Up CentOS 7 Virtual Machine**

#### **Virtual Machine Creation Wizard**
```
┌─────────────────────────────────────────────────────────────────┐
│                  Creating New Virtual Machine                  │
└─────────────────────────────────────────────────────────────────┘

Step-by-Step VM Creation:

1️⃣ Launch VM Creation:
   File → New Virtual Machine → Custom (advanced)
   
2️⃣ Hardware Compatibility:
   ┌─────────────────────────────────────────────────────────────┐
   │ Hardware compatibility: Workstation 17.x                   │
   │ Benefits: Latest features, best performance                 │
   │ Choose: Workstation 17.x (recommended)                     │
   └─────────────────────────────────────────────────────────────┘

3️⃣ Guest Operating System:
   ┌─────────────────────────────────────────────────────────────┐
   │ Installation source:                                        │
   │ ○ Installer disc image file (iso): [Browse to CentOS ISO]  │
   │ ○ I will install the operating system later               │
   │                                                             │
   │ Recommendation: Choose "I will install later" for manual   │
   │ control over installation process                           │
   └─────────────────────────────────────────────────────────────┘

4️⃣ Guest OS Selection:
   ┌─────────────────────────────────────────────────────────────┐
   │ Guest operating system: ● Linux                            │
   │ Version: Red Hat Enterprise Linux 7 64-bit                 │
   │                                                             │
   │ Note: CentOS 7 is RHEL-compatible, so use RHEL 7 setting  │
   └─────────────────────────────────────────────────────────────┘
```

#### **VM Configuration Settings**
```
5️⃣ Virtual Machine Name and Location:
   ┌─────────────────────────────────────────────────────────────┐
   │ Virtual machine name: CentOS7-Server-Lab                   │
   │ Location: D:\VirtualMachines\VMs\CentOS7-Server-Lab\      │
   │                                                             │
   │ Naming Convention Tips:                                     │
   │ • Include OS version and purpose                           │
   │ • Use descriptive names for multiple VMs                  │
   │ • Avoid spaces (use hyphens or underscores)               │
   └─────────────────────────────────────────────────────────────┘

6️⃣ Processor Configuration:
   ┌─────────────────────────────────────────────────────────────┐
   │ Number of processors: 1                                    │
   │ Number of cores per processor: 2                           │
   │                                                             │
   │ Recommendations by use case:                               │
   │ • Learning/Basic: 1 processor, 1-2 cores                  │
   │ • Development: 1 processor, 2-4 cores                     │
   │ • Server simulation: 2 processors, 2 cores each           │
   │                                                             │
   │ ✅ Virtualize Intel VT-x/EPT or AMD-V/RVI                │
   │ ✅ Virtualize CPU performance counters                    │
   └─────────────────────────────────────────────────────────────┘

7️⃣ Memory Configuration:
   ┌─────────────────────────────────────────────────────────────┐
   │ Memory for this virtual machine: 2048 MB                   │
   │                                                             │
   │ Memory Allocation Guidelines:                               │
   │ • Minimal CentOS: 1GB (1024 MB)                           │
   │ • Server with GUI: 2GB (2048 MB) ⭐                       │
   │ • Development environment: 4GB (4096 MB)                   │
   │ • Production simulation: 8GB+ (8192 MB)                    │
   │                                                             │
   │ Rule: Don't exceed 75% of host physical RAM                │
   └─────────────────────────────────────────────────────────────┘
```

#### **Storage and Network Configuration**
```
8️⃣ Network Type:
   ┌─────────────────────────────────────────────────────────────┐
   │ Network connection: ● Use network address translation (NAT) │
   │                                                             │
   │ Network Options Explained:                                  │
   │ • NAT: VM gets internet, host protection ⭐                │
   │ • Bridged: VM appears as separate device on network        │
   │ • Host-only: VM communicates only with host                │
   │ • Custom: Advanced networking scenarios                     │
   └─────────────────────────────────────────────────────────────┘

9️⃣ I/O Controller Types:
   ┌─────────────────────────────────────────────────────────────┐
   │ SCSI Controller: LSI Logic (Recommended) ⭐                 │
   │ IDE Controller: Use for older OS compatibility only        │
   │                                                             │
   │ Performance ranking: NVMe > SCSI > IDE                     │
   └─────────────────────────────────────────────────────────────┘

🔟 Virtual Disk Configuration:
   ┌─────────────────────────────────────────────────────────────┐
   │ Disk Type: ● Create a new virtual disk                     │
   │ Virtual disk type: ● SCSI (Recommended)                    │
   │                                                             │
   │ Disk size: 20.0 GB                                        │
   │ ○ Allocate all disk space now (better performance)         │
   │ ● Split virtual disk into multiple files (portable)        │
   │                                                             │
   │ Disk Size Recommendations:                                  │
   │ • Minimal install: 10GB minimum                           │
   │ • Server with packages: 20GB ⭐                           │
   │ • Development environment: 40GB+                           │
   │ • Desktop with applications: 60GB+                         │
   └─────────────────────────────────────────────────────────────┘
```

#### **Hardware Customization**
```
Advanced Hardware Configuration:

🔧 Customize Hardware Settings:
Before powering on, click "Customize Hardware":

┌─────────────────────────────────────────────────────────────────┐
│ Component          │ Recommended Setting                        │
├────────────────────┼────────────────────────────────────────────┤
│ Memory             │ 2048 MB (adjust based on host capacity)   │
│ Processors         │ 2 cores (enable virtualization features)  │
│ Hard Disk          │ 20 GB, SCSI, split files                  │
│ CD/DVD (IDE)       │ Use ISO image file: [CentOS ISO path]     │
│ Network Adapter    │ NAT, Connect at power on ✅               │
│ USB Controller     │ USB 3.1 (for better device support)       │
│ Sound Card         │ Remove (not needed for server)            │
│ Display            │ Auto detect, 3D acceleration ✅           │
└────────────────────┴────────────────────────────────────────────┘

⚙️ Advanced Options:
Settings → Advanced:
• Firmware type: UEFI (modern standard)
• Boot options: EFI boot
• Side channel mitigations: Enable (security)

🎯 Performance Optimization:
Settings → Options → VMware Tools:
• Synchronize guest time with host ✅
• Update automatically ✅

Settings → Options → Advanced:
• Enable logging: Disable (performance)
• Configuration parameters: Add if needed
```

---

## 💽 CentOS 7 Installation Process

### **Complete CentOS 7 Installation Walkthrough**

#### **Starting the Installation**
```
┌─────────────────────────────────────────────────────────────────┐
│                CentOS 7 Installation Boot Process              │
└─────────────────────────────────────────────────────────────────┘

🚀 Boot Sequence:
1. Power on the virtual machine
2. CentOS 7 boot menu appears:

   ┌─────────────────────────────────────────────────────────────┐
   │                    CentOS Linux 7                           │
   │                                                             │
   │ Install CentOS 7                          ⭐ (Select this) │
   │ Test this media & install CentOS 7                         │
   │ Troubleshooting →                                           │
   │                                                             │
   │ Press TAB to edit options                                   │
   │ Automatic boot in 60 seconds...                            │
   └─────────────────────────────────────────────────────────────┘

3. Loading process begins:
   • Initial ramdisk loading
   • Hardware detection
   • Anaconda installer startup

💡 Installation Boot Options:
   Standard Install: Press Enter (recommended)
   Text Mode: Add 'text' to boot parameters
   VNC Install: Add 'vnc' for remote installation
   Serial Console: Add 'console=ttyS0' for headless
```

#### **Language and Localization Settings**
```
🌍 Welcome Screen Configuration:

┌─────────────────────────────────────────────────────────────────┐
│                  WELCOME TO CENTOS 7                           │
│                                                                 │
│ What language would you like to use during the installation    │
│ process?                                                        │
│                                                                 │
│ English (United States) ⭐                                     │
│ العربية (Arabic)                                                │
│ Български (Bulgarian)                                           │
│ 中文 (Chinese Simplified)                                       │
│ Čeština (Czech)                                                 │
│ Dansk (Danish)                                                  │
│ [Continue]                                                      │
└─────────────────────────────────────────────────────────────────┘

Language Selection Impact:
• Installer interface language
• Default system locale
• Keyboard layout suggestions
• Time zone pre-selection
• Package group descriptions

Recommendation: Choose your native language for better understanding
```

#### **Installation Summary Hub**
```
🎛️ Installation Summary Screen:

┌─────────────────────────────────────────────────────────────────┐
│                    INSTALLATION SUMMARY                        │
│                                                                 │
│ LOCALIZATION                    │ SOFTWARE                     │
│ ┌─────────────────────────────┐ │ ┌─────────────────────────────┐ │
│ │ DATE & TIME                 │ │ │ INSTALLATION SOURCE         │ │
│ │ Americas/New_York timezone  │ │ │ Local media                 │ │
│ └─────────────────────────────┘ │ └─────────────────────────────┘ │
│ ┌─────────────────────────────┐ │ ┌─────────────────────────────┐ │
│ │ KEYBOARD                    │ │ │ SOFTWARE SELECTION          │ │
│ │ English (US)                │ │ │ Minimal Install ⚠️          │ │
│ └─────────────────────────────┘ │ └─────────────────────────────┘ │
│ ┌─────────────────────────────┐ │                               │
│ │ LANGUAGE SUPPORT            │ │ SYSTEM                        │
│ │ English (United States)     │ │ ┌─────────────────────────────┐ │
│ └─────────────────────────────┘ │ │ INSTALLATION DESTINATION    │ │
│                                 │ │ Automatic partitioning ⚠️   │ │
│                                 │ └─────────────────────────────┘ │
│                                 │ ┌─────────────────────────────┐ │
│                                 │ │ NETWORK & HOST NAME         │ │
│                                 │ │ Not connected ⚠️            │ │
│                                 │ └─────────────────────────────┘ │
│                                                                 │
│ [Begin Installation] (disabled until warnings resolved)        │
└─────────────────────────────────────────────────────────────────┘

⚠️ Items marked with warning triangles require configuration!
```

---

## 🗂️ Understanding Linux Partitioning

### **Linux File System Partitioning Fundamentals**

#### **Partition Concepts for Beginners**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Linux Partitioning Basics                   │
└─────────────────────────────────────────────────────────────────┘

What is Partitioning?
Think of your hard drive as a large empty warehouse:

🏢 Physical Hard Drive (20GB):
┌─────────────────────────────────────────────────────────────────┐
│                    Raw Unpartitioned Space                     │
│                         20GB Available                         │
└─────────────────────────────────────────────────────────────────┘

After Partitioning:
┌─────────────────────────────────────────────────────────────────┐
│ /boot    │            /            │    swap    │   /home      │
│  500MB   │           15GB          │    2GB     │    2.5GB     │
│          │                         │            │              │
│ Boot     │    System Files         │  Virtual   │    User      │
│ Files    │    Programs, OS         │  Memory    │    Data      │
└─────────────────────────────────────────────────────────────────┘

Why Partition?
✅ Organization: Separate system from user data
✅ Security: Isolate sensitive areas
✅ Performance: Optimize different areas differently
✅ Backup: Back up different areas separately
✅ Recovery: Reinstall OS without losing user data
```

#### **Essential Linux Partitions**
```
🗂️ Required and Recommended Partitions:

┌─────────────────────────────────────────────────────────────────┐
│ Partition │ Mount Point │ Size      │ Purpose                   │
├───────────┼─────────────┼───────────┼───────────────────────────┤
│ /boot     │ /boot       │ 500MB     │ Boot loader and kernels   │
│ /         │ /           │ 10-15GB   │ Root filesystem (system)  │
│ swap      │ [swap]      │ 1-2GB     │ Virtual memory           │
│ /home     │ /home       │ Remaining │ User data and configs     │
└───────────┴─────────────┴───────────┴───────────────────────────┘

🏠 Partition Purposes Explained:

/boot Partition:
• Contains kernel files and boot loader
• Must be readable by BIOS/UEFI
• Separate partition ensures bootability
• Size: 500MB-1GB (plenty for multiple kernels)

/ (Root) Partition:
• Contains entire operating system
• All system files, programs, libraries
• Like C:\ drive in Windows
• Size: 10GB minimum, 15-20GB recommended

swap Partition:
• Virtual memory extension of RAM
• Used when physical RAM is full
• Hibernation support (if used)
• Size: 1-2x RAM size (for systems with <8GB RAM)

/home Partition:
• User directories and personal files
• Survives OS reinstallation
• Like "Users" folder in Windows
• Size: All remaining space
```

#### **Partitioning Schemes Comparison**
```
🎯 Partitioning Strategy Options:

Option 1: Automatic/Simple (Beginner):
┌─────────────────────────────────────────────────────────────────┐
│ /boot: 500MB │           /: 17.5GB          │    swap: 2GB     │
│              │  (includes /home in root)    │                  │
└─────────────────────────────────────────────────────────────────┘
Pros: Simple, less to manage
Cons: User data mixed with system

Option 2: Standard Server (Recommended):
┌─────────────────────────────────────────────────────────────────┐
│ /boot │        /        │  swap  │         /home               │
│ 500MB │      12GB       │  2GB   │         5.5GB               │
└─────────────────────────────────────────────────────────────────┘
Pros: Data separation, easier backup
Cons: Need to estimate sizes

Option 3: Advanced/Production:
┌─────────────────────────────────────────────────────────────────┐
│ /boot │ / │ /var │ /tmp │ swap │ /home │ /opt │ /usr/local    │
│ 500MB │8GB│ 4GB  │ 1GB  │ 2GB  │ 2GB   │ 1GB  │ 1.5GB         │
└─────────────────────────────────────────────────────────────────┘
Pros: Maximum control and security
Cons: Complex sizing decisions

🎯 rootguru Recommendation for Learning:
Use Option 2 (Standard Server) - provides good balance of
simplicity and real-world applicability.
```

---

## 🛠️ Manual Partitioning Setup

### **Step-by-Step Manual Partitioning Configuration**

#### **Accessing Manual Partitioning**
```
🔧 Installation Destination Configuration:

From Installation Summary → INSTALLATION DESTINATION:

┌─────────────────────────────────────────────────────────────────┐
│                    INSTALLATION DESTINATION                     │
│                                                                 │
│ Select the device(s) you would like to install to and the      │
│ options you would like to use.                                 │
│                                                                 │
│ Local Standard Disks:                                          │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ ✅ VMware Virtual disk 20 GiB                               │ │
│ │    Free Space: 20 GiB                                      │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ Partitioning:                                                  │
│ ○ Automatically configure partitioning                         │
│ ● I will configure partitioning ⭐                            │
│                                                                 │
│ ✅ I would like to make additional space available             │
│                                                                 │
│ [Done]                                                          │
└─────────────────────────────────────────────────────────────────┘

Click "Done" to proceed to manual partitioning screen.
```

#### **Manual Partitioning Interface**
```
🎛️ Manual Partitioning Screen:

┌─────────────────────────────────────────────────────────────────┐
│                    MANUAL PARTITIONING                         │
│                                                                 │
│ New CentOS 7 Installation                                      │
│                                                                 │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │                    Mount Points                             │ │
│ │                                                             │ │
│ │ (Empty - we'll create partitions)                          │ │
│ │                                                             │ │
│ │                                                             │ │
│ │                                                             │ │
│ │ [+] Click here to create them automatically                │ │
│ │                                                             │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ New mount point:                                               │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ /boot                                      [+]             │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ Available Space: 20 GiB                                       │
│                                                                 │
│ [Done]     [Reset]                                             │
└─────────────────────────────────────────────────────────────────┘

Partitioning Strategy: We'll create each partition manually for learning
```

#### **Creating the /boot Partition**
```
1️⃣ Creating /boot Partition:

In "New mount point" field: type "/boot" → Click [+]

┌─────────────────────────────────────────────────────────────────┐
│                    ADD A NEW MOUNT POINT                       │
│                                                                 │
│ Mount Point: /boot                                             │
│                                                                 │
│ Desired Capacity: 500 MiB                                      │
│                                                                 │
│ Device Type: ● Standard Partition                              │
│              ○ LVM                                             │
│              ○ BTRFS                                           │
│                                                                 │
│ File System: ● ext4                                            │
│              ○ ext3                                            │
│              ○ xfs                                             │
│              ○ vfat                                            │
│                                                                 │
│ [Add mount point]                                              │
└─────────────────────────────────────────────────────────────────┘

✅ Settings Explanation:
• Mount Point: /boot (where boot files live)
• Capacity: 500 MiB (plenty for kernels and initrd)
• Device Type: Standard Partition (simple and reliable)
• File System: ext4 (stable, widely supported)
```

#### **Creating the Swap Partition**
```
2️⃣ Creating Swap Partition:

In "New mount point" field: leave empty (or type "swap") → Click [+]

┌─────────────────────────────────────────────────────────────────┐
│                    ADD A NEW MOUNT POINT                       │
│                                                                 │
│ Mount Point: [leave empty for swap]                           │
│                                                                 │
│ Desired Capacity: 2 GiB                                       │
│                                                                 │
│ Device Type: ● Standard Partition                              │
│              ○ LVM                                             │
│              ○ BTRFS                                           │
│                                                                 │
│ File System: ● swap                                            │
│              ○ ext4                                            │
│              ○ ext3                                            │
│              ○ xfs                                             │
│                                                                 │
│ [Add mount point]                                              │
└─────────────────────────────────────────────────────────────────┘

✅ Swap Sizing Guidelines:
• 2GB VM RAM → 2GB swap (1:1 ratio)
• For hibernation: swap ≥ RAM size
• Modern systems with >8GB RAM: 2-4GB swap sufficient
• Server without hibernation: 1-2GB adequate
```

#### **Creating the Root (/) Partition**
```
3️⃣ Creating Root Partition:

In "New mount point" field: type "/" → Click [+]

┌─────────────────────────────────────────────────────────────────┐
│                    ADD A NEW MOUNT POINT                       │
│                                                                 │
│ Mount Point: /                                                 │
│                                                                 │
│ Desired Capacity: 12 GiB                                      │
│                                                                 │
│ Device Type: ● Standard Partition                              │
│              ○ LVM                                             │
│              ○ BTRFS                                           │
│                                                                 │
│ File System: ● xfs                                             │
│              ○ ext4                                            │
│              ○ ext3                                            │
│              ○ btrfs                                           │
│                                                                 │
│ [Add mount point]                                              │
└─────────────────────────────────────────────────────────────────┘

✅ Root Partition Notes:
• Mount Point: / (root of entire filesystem)
• Capacity: 12 GiB (adequate for system and programs)
• File System: xfs (RHEL/CentOS 7 default, excellent performance)
• Contains: /bin, /etc, /lib, /usr, /var (unless separate)
```

#### **Creating the /home Partition**
```
4️⃣ Creating /home Partition:

In "New mount point" field: type "/home" → Click [+]

┌─────────────────────────────────────────────────────────────────┐
│                    ADD A NEW MOUNT POINT                       │
│                                                                 │
│ Mount Point: /home                                             │
│                                                                 │
│ Desired Capacity: [leave empty for remaining space]           │
│                                                                 │
│ Device Type: ● Standard Partition                              │
│              ○ LVM                                             │
│              ○ BTRFS                                           │
│                                                                 │
│ File System: ● xfs                                             │
│              ○ ext4                                            │
│              ○ ext3                                            │
│              ○ btrfs                                           │
│                                                                 │
│ [Add mount point]                                              │
└─────────────────────────────────────────────────────────────────┘

✅ /home Partition Benefits:
• User data separation from system
• Survives OS reinstallation
• Individual user quotas possible
• Easier backup strategy
• Uses remaining space automatically
```

#### **Reviewing Partition Layout**
```
📋 Final Partition Review:

After creating all partitions, your layout should look like:

┌─────────────────────────────────────────────────────────────────┐
│                    MANUAL PARTITIONING                         │
│                                                                 │
│ New CentOS 7 Installation                                      │
│                                                                 │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ /boot     sda1    ext4     500 MiB                         │ │
│ │ /         sda2    xfs      12 GiB                          │ │
│ │ /home     sda3    xfs      5.5 GiB                         │ │
│ │ [swap]    sda4    swap     2 GiB                           │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ Available Space: 0 B                                          │
│                                                                 │
│ [Done]     [Reset]                                             │
└─────────────────────────────────────────────────────────────────┘

✅ Verification Checklist:
□ /boot partition exists (500MB, ext4)
□ / partition exists (12GB, xfs) 
□ swap partition exists (2GB, swap)
□ /home partition exists (remaining space, xfs)
□ Total space allocated = 20GB
□ No overlapping partitions

Click [Done] to accept the partitioning scheme.
```

---

## 🌐 Network Configuration

### **Configuring Network Settings During Installation**

#### **Network & Host Name Configuration**
```
🌍 Network Configuration Screen:

From Installation Summary → NETWORK & HOST NAME:

┌─────────────────────────────────────────────────────────────────┐
│                    NETWORK & HOST NAME                         │
│                                                                 │
│ Ethernet (ens33)                               [OFF] → [ON] ⭐ │
│                                                                 │
│ Host name: localhost.localdomain                               │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ centos7-server.rootguru.lab                                 │ │
│ └─────────────────────────────────────────────────────────────┘ │
│ [Apply]                                                        │
│                                                                 │
│ When ethernet is ON:                                           │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ Wired connection 1                                          │ │
│ │ IPv4: 192.168.xxx.xxx/24                                   │ │
│ │ IPv6: fe80::xxxx:xxxx:xxxx:xxxx/64                         │ │
│ │ Default route: 192.168.xxx.1                               │ │
│ │ DNS: 192.168.xxx.1                                         │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ [Configure...]                                                 │
│ [Done]                                                          │
└─────────────────────────────────────────────────────────────────┘

🎯 Essential Network Setup Steps:
1. Turn Ethernet adapter ON (slide switch)
2. Set meaningful hostname
3. Verify automatic IP configuration
4. Configure manual settings if needed
```

#### **Manual Network Configuration**
```
🔧 Advanced Network Settings:

Click [Configure...] for detailed network settings:

┌─────────────────────────────────────────────────────────────────┐
│                  Editing Wired Connection 1                    │
│                                                                 │
│ Connection name: Wired connection 1                            │
│ ✅ Connect automatically                                       │
│ ✅ Available to all users                                      │
│                                                                 │
│ Tabs: [General] [Ethernet] [802.1X] [DCB] [Proxy]            │
│       [IPv4 Settings] [IPv6 Settings]                         │
│                                                                 │
│ IPv4 Settings:                                                 │
│ Method: ● Automatic (DHCP) ⭐                                  │
│         ○ Manual                                               │
│         ○ Link-Local Only                                      │
│         ○ Disabled                                             │
│                                                                 │
│ For Manual Configuration:                                       │
│ Addresses:                                                     │
│ ┌─────────────────┬─────────────┬─────────────────────────────┐ │
│ │ Address         │ Netmask     │ Gateway                     │ │
│ ├─────────────────┼─────────────┼─────────────────────────────┤ │
│ │ 192.168.1.100   │ 24          │ 192.168.1.1                │ │
│ └─────────────────┴─────────────┴─────────────────────────────┘ │
│                                                                 │
│ DNS servers: 8.8.8.8, 8.8.4.4                                │
│ Search domains: rootguru.lab                                  │
│                                                                 │
│ [Save]                                                         │
└─────────────────────────────────────────────────────────────────┘
```

#### **Hostname Configuration Best Practices**
```
🏷️ Hostname Configuration Guidelines:

Recommended Naming Convention:
┌─────────────────────────────────────────────────────────────────┐
│ Format: [role]-[os][version]-[instance].[domain]              │
│                                                                 │
│ Examples:                                                       │
│ • web01-centos7-001.rootguru.lab                              │
│ • db-server-centos7.internal.local                            │
│ • centos7-desktop.lab.local                                   │
│ • test-vm-centos7.example.com                                 │
└─────────────────────────────────────────────────────────────────┘

Hostname Rules:
✅ Use lowercase letters
✅ Include numbers and hyphens
✅ Start with letter
✅ End with letter or number
✅ Maximum 63 characters per label
❌ No spaces or special characters
❌ Don't start with number
❌ Don't use underscore in hostname

🎯 For This Lab:
Hostname: centos7-server.rootguru.lab
Benefits:
• Clearly identifies OS and purpose
• Uses lab domain for isolation
• Professional naming convention
• Easy to remember and type
```

#### **Network Troubleshooting in VMware**
```
🔧 Common VMware Network Issues:

Issue 1: No Network Connectivity
┌─────────────────────────────────────────────────────────────────┐
│ Symptoms: No IP address, can't ping gateway                    │
│                                                                 │
│ Solutions:                                                      │
│ 1. Check VM network adapter connection:                        │
│    VM Settings → Network Adapter → Connected ✅               │
│                                                                 │
│ 2. Verify network adapter type:                               │
│    Recommended: NAT (for internet access)                      │
│                                                                 │
│ 3. Check VMware services (Windows host):                      │
│    Services.msc → VMware DHCP Service → Running               │
│    Services.msc → VMware NAT Service → Running                │
│                                                                 │
│ 4. Reset VMware networking:                                    │
│    Edit → Virtual Network Editor → Restore Defaults           │
└─────────────────────────────────────────────────────────────────┘

Issue 2: IP Address Conflicts
┌─────────────────────────────────────────────────────────────────┐
│ Symptoms: Internet works sometimes, connection drops           │
│                                                                 │
│ Solutions:                                                      │
│ 1. Check DHCP lease time:                                     │
│    Edit → Virtual Network Editor → NAT Settings → DHCP        │
│                                                                 │
│ 2. Reserve IP addresses:                                       │
│    Configure static IPs outside DHCP range                     │
│                                                                 │
│ 3. Restart DHCP service:                                       │
│    Edit → Virtual Network Editor → NAT Settings → Stop/Start  │
└─────────────────────────────────────────────────────────────────┘
```

---

## ⚙️ Initial System Configuration

### **Post-Installation Basic Configuration**

#### **Software Selection**
```
📦 Software Selection Screen:

From Installation Summary → SOFTWARE SELECTION:

┌─────────────────────────────────────────────────────────────────┐
│                    SOFTWARE SELECTION                          │
│                                                                 │
│ Base Environment:                                              │
│ ○ Minimal Install                                             │
│ ● Server with GUI ⭐                                          │
│ ○ GNOME Desktop                                               │
│ ○ KDE Plasma Workspaces                                       │
│ ○ Virtualization Host                                         │
│ ○ Infrastructure Server                                        │
│ ○ File and Print Server                                       │
│ ○ Basic Web Server                                            │
│                                                                 │
│ Add-ons for Selected Environment:                             │
│ ✅ Development Tools                                           │
│ ✅ System Administration Tools                                 │
│ ○ Security Tools                                              │
│ ○ Smart Card Support                                          │
│ ○ Remote Desktop Clients                                      │
│ ○ Additional Development                                       │
│                                                                 │
│ [Done]                                                         │
└─────────────────────────────────────────────────────────────────┘

🎯 Recommended Selection: "Server with GUI"
Benefits:
• Command line and graphical interface
• Essential server packages included
• Good balance for learning
• Easy transition between CLI and GUI
```

#### **Root Password and User Creation**
```
👤 User Configuration Screen:

During installation, you'll see:

┌─────────────────────────────────────────────────────────────────┐
│                    CONFIGURATION                               │
│                                                                 │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ ROOT PASSWORD                                               │ │
│ │ The root account is used for administering the system      │ │
│ │ Enter a password for the root user.                        │ │
│ │                                                             │ │
│ │ Root password: ●●●●●●●●●●●●                                 │ │
│ │ Confirm: ●●●●●●●●●●●●                                       │ │
│ │                                                             │ │
│ │ ⚠️ The password you have provided is weak                  │ │
│ │ □ Allow weak password                                       │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ USER CREATION                                               │ │
│ │ Create a user account for yourself                          │ │
│ │                                                             │ │
│ │ Full name: System Administrator                             │ │
│ │ User name: sysadmin                                        │ │
│ │ ✅ Make this user administrator                            │ │
│ │ ✅ Require a password to use this account                  │ │
│ │                                                             │ │
│ │ Password: ●●●●●●●●●●●●                                      │ │
│ │ Confirm: ●●●●●●●●●●●●                                       │ │
│ └─────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘

🔐 Security Best Practices:
Root Password:
• Use strong password (12+ characters)
• Include uppercase, lowercase, numbers, symbols
• Don't use dictionary words
• Example: R00tGuru2024!Lab

User Account:
• Create admin user for daily use
• Use descriptive username (sysadmin, admin, yourname)
• Enable "Make this user administrator" (sudo access)
• Use different password than root
```

#### **Installation Progress and Completion**
```
⏳ Installation Progress:

┌─────────────────────────────────────────────────────────────────┐
│                    INSTALLATION PROGRESS                       │
│                                                                 │
│ Installing CentOS 7...                                         │
│                                                                 │
│ ████████████████████████████████████████████ 85%              │
│                                                                 │
│ Installing @gnome-desktop (254/312)                           │
│ Installing libproxy-0.4.11-8.el7.x86_64                      │
│                                                                 │
│ Post-installation setup running...                             │
│                                                                 │
│ Setting up users and groups...                                 │
│ Configuring installed system...                                │
│ Writing network configuration...                                │
│ Creating initramfs...                                          │
│                                                                 │
│ Time remaining: ~ 8 minutes                                    │
│                                                                 │
│ [Installation Progress Log]                                    │
└─────────────────────────────────────────────────────────────────┘

Installation phases:
1. Package installation (longest phase)
2. System configuration
3. User and group setup
4. Network configuration
5. Boot loader installation
6. Post-installation scripts

⏱️ Typical installation time: 15-45 minutes
(Depends on: VM resources, host performance, selected packages)
```

---

## 🔧 Post-Installation Tasks

### **Essential First Boot Configuration**

#### **Initial Boot and Setup**
```
🚀 First Boot Sequence:

After installation completion:

1️⃣ Reboot Process:
┌─────────────────────────────────────────────────────────────────┐
│                    Installation Complete!                      │
│                                                                 │
│ Congratulations! Your CentOS installation is complete.         │
│                                                                 │
│ Please reboot to start using your CentOS system.              │
│                                                                 │
│ Don't forget to eject the installation media!                  │
│                                                                 │
│ [Reboot]                                                       │
└─────────────────────────────────────────────────────────────────┘

2️⃣ Remove Installation Media:
   VM Settings → CD/DVD → Use physical drive (auto detect)
   Or: Disconnect ISO file

3️⃣ First Boot Messages:
   • GRUB bootloader appears
   • Kernel loading messages
   • Service startup messages
   • Login screen appears
```

#### **Initial Welcome Setup**
```
🎉 Initial Setup Wizard (if using GUI):

┌─────────────────────────────────────────────────────────────────┐
│                       Welcome                                   │
│                                                                 │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ License Information                                         │ │
│ │ Please review and accept the license agreement             │ │
│ │                                                             │ │
│ │ ✅ I accept the license agreement                          │ │
│ │                                                             │ │
│ │ [Done]                                                      │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ [Begin Using CentOS]                                           │
└─────────────────────────────────────────────────────────────────┘

🔧 Complete the initial setup:
1. Accept license agreement
2. Click "Begin Using CentOS"
3. Login with created user account
4. Desktop environment loads
```

#### **First Login and Basic Commands**
```
💻 First Login Session:

Terminal Commands to Verify Installation:

# Check system information
uname -a
# Output: Linux centos7-server.rootguru.lab 3.10.0-1160.el7.x86_64 ...

# Check CentOS version
cat /etc/redhat-release
# Output: CentOS Linux release 7.9.2009 (Core)

# Check IP address
ip addr show
# Look for: inet 192.168.xxx.xxx/24

# Check disk usage
df -h
# Verify partitions are mounted correctly

# Check memory
free -h
# Verify RAM allocation

# Check network connectivity
ping -c 3 google.com
# Should show successful ping responses

# Check hostname
hostname
hostname -f
# Should show: centos7-server.rootguru.lab

# Check running services
systemctl status NetworkManager
systemctl status sshd

# Update system (requires internet)
sudo yum update -y
```

#### **Essential System Updates**
```
📦 Post-Installation Updates:

# 1. Update all packages to latest versions:
sudo yum update -y

# This updates:
# - Kernel (security patches)
# - All installed packages
# - Security updates
# - Bug fixes

# 2. Install additional useful packages:
sudo yum install -y epel-release
sudo yum install -y vim wget curl tree htop net-tools

# Package purposes:
# epel-release: Extra packages repository
# vim: Advanced text editor
# wget/curl: Download tools
# tree: Directory tree view
# htop: Better process monitor
# net-tools: Network utilities (ifconfig, netstat)

# 3. Enable useful services:
sudo systemctl enable sshd
sudo systemctl start sshd

# 4. Configure firewall (if needed):
sudo systemctl status firewalld
sudo firewall-cmd --list-all

# 5. Set timezone (if not correct):
sudo timedatectl set-timezone America/New_York
timedatectl status
```

---

## 🛠️ VMware Tools Installation

### **Installing VMware Tools for Better Performance**

#### **VMware Tools Benefits and Installation**
```
🚀 VMware Tools Benefits:

┌─────────────────────────────────────────────────────────────────┐
│                      VMware Tools Features                     │
│                                                                 │
│ Performance Improvements:                                       │
│ ✅ Better graphics performance                                 │
│ ✅ Improved memory management                                  │
│ ✅ Enhanced network performance                                │
│ ✅ Optimized disk I/O                                         │
│                                                                 │
│ Usability Features:                                            │
│ ✅ Seamless mouse integration                                  │
│ ✅ Clipboard sharing (copy/paste)                             │
│ ✅ Automatic screen resolution                                 │
│ ✅ Drag and drop files                                        │
│ ✅ Shared folders access                                       │
│                                                                 │
│ Management Features:                                            │
│ ✅ Time synchronization                                        │
│ ✅ Graceful shutdown/restart                                   │
│ ✅ VM heartbeat monitoring                                     │
│ ✅ Guest customization support                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### **Installing VMware Tools**
```
🔧 VMware Tools Installation Process:

Method 1: Automatic Installation (Recommended):
1️⃣ From VMware Workstation menu:
   VM → Install VMware Tools...

2️⃣ Virtual DVD is mounted automatically:
   /dev/sr0 or /run/media/[user]/VMware Tools

3️⃣ Open terminal and run installation:
# Mount the DVD (if not auto-mounted)
sudo mkdir -p /mnt/cdrom
sudo mount /dev/sr0 /mnt/cdrom

# Copy installer to temp directory
cp /mnt/cdrom/VMwareTools-*.tar.gz /tmp/

# Extract the installer
cd /tmp
tar -xzf VMwareTools-*.tar.gz

# Run the installer
cd vmware-tools-distrib
sudo ./vmware-install.pl

# Accept all defaults by pressing Enter for each prompt
# Installation process:
# - Kernel modules compilation
# - Service configuration
# - Feature enablement

# Reboot after installation
sudo reboot

Method 2: Open VM Tools (Modern Alternative):
# CentOS 7 includes open-vm-tools by default
sudo yum install -y open-vm-tools open-vm-tools-desktop

# Enable and start services
sudo systemctl enable vmtoolsd
sudo systemctl start vmtoolsd

# Reboot to activate all features
sudo reboot
```

#### **Verifying VMware Tools Installation**
```
✅ Verification Commands:

# Check VMware Tools status
vmware-toolbox-cmd -v
# Output: 11.x.x.xxxxx (build-xxxxxxx)

# Check running services
sudo systemctl status vmtoolsd
# Should show: active (running)

# Test clipboard sharing
# Copy text in host OS, try pasting in VM

# Test mouse integration
# Mouse should move seamlessly between host and guest

# Check shared folders (if configured)
vmware-hgfsclient
# Lists available shared folders

# Test time synchronization
sudo vmware-toolbox-cmd timesync status
# Should show: Enabled

# Check guest info
vmware-toolbox-cmd stat raw text session
# Shows various VM statistics

🎯 Troubleshooting VMware Tools Issues:

Issue: Tools not working after kernel update
Solution: Reinstall VMware Tools or open-vm-tools

Issue: Mouse/keyboard not working properly
Solution: Restart vmtoolsd service
sudo systemctl restart vmtoolsd

Issue: Shared folders not accessible
Solution: Check VM settings and remount
```

---

## 🌐 Network Troubleshooting

### **Common Network Issues and Solutions**

#### **Network Connectivity Troubleshooting**
```
🔍 Network Troubleshooting Methodology:

Step-by-Step Network Diagnosis:

1️⃣ Check Physical/Virtual Connectivity:
# Verify VM network adapter is connected
# VM Settings → Network Adapter → Connected ✅

# Check interface status
ip link show
# Look for: state UP

# Check if interface has IP address
ip addr show ens33
# Should show: inet 192.168.xxx.xxx/24

2️⃣ Test Local Network Stack:
# Test loopback interface
ping 127.0.0.1

# Test local IP
ping $(hostname -I | awk '{print $1}')

3️⃣ Test Gateway Connectivity:
# Find default gateway
ip route | grep default
# Output: default via 192.168.xxx.1 dev ens33

# Test gateway
ping -c 3 192.168.xxx.1

4️⃣ Test DNS Resolution:
# Test with IP address
ping -c 3 8.8.8.8

# Test with hostname
ping -c 3 google.com

# Check DNS configuration
cat /etc/resolv.conf
```

#### **Common Network Problems and Solutions**
```
🚨 Problem 1: No IP Address (DHCP Not Working)

Symptoms:
• ip addr shows no IP on ens33
• Cannot ping gateway
• No internet connectivity

Diagnosis:
# Check NetworkManager status
sudo systemctl status NetworkManager

# Check DHCP client
sudo journalctl -u NetworkManager | grep DHCP

Solutions:
# Restart NetworkManager
sudo systemctl restart NetworkManager

# Restart network interface
sudo nmcli connection down "System ens33"
sudo nmcli connection up "System ens33"

# Manual DHCP request
sudo dhclient ens33

# Check VMware DHCP service (host side)
# Services.msc → VMware DHCP Service → Restart

🚨 Problem 2: DNS Resolution Failing

Symptoms:
• Can ping IP addresses (8.8.8.8)
• Cannot ping hostnames (google.com)
• curl/wget fail with hostname errors

Diagnosis:
# Check DNS servers
cat /etc/resolv.conf

# Test specific DNS server
nslookup google.com 8.8.8.8

Solutions:
# Add reliable DNS servers
echo "nameserver 8.8.8.8" | sudo tee -a /etc/resolv.conf
echo "nameserver 8.8.4.4" | sudo tee -a /etc/resolv.conf

# Or configure through NetworkManager
sudo nmcli connection modify "System ens33" ipv4.dns "8.8.8.8,8.8.4.4"
sudo nmcli connection up "System ens33"

🚨 Problem 3: Firewall Blocking Connections

Symptoms:
• Local connectivity works
• Some external connections fail
• Services not accessible from outside

Diagnosis:
# Check firewall status
sudo firewall-cmd --state

# List active rules
sudo firewall-cmd --list-all

Solutions:
# Temporarily disable firewall for testing
sudo systemctl stop firewalld

# If connectivity works, add necessary rules:
sudo systemctl start firewalld
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
```

#### **Network Configuration Files**
```
📁 Important Network Configuration Files:

# Main network configuration
/etc/sysconfig/network-scripts/ifcfg-ens33
┌─────────────────────────────────────────────────────────────────┐
│ TYPE=Ethernet                                                   │
│ BOOTPROTO=dhcp                                                  │
│ DEFROUTE=yes                                                    │
│ NAME=ens33                                                      │
│ DEVICE=ens33                                                    │
│ ONBOOT=yes                                                      │
│ DNS1=8.8.8.8                                                    │
│ DNS2=8.8.4.4                                                    │
└─────────────────────────────────────────────────────────────────┘

# Hostname configuration
/etc/hostname
┌─────────────────────────────────────────────────────────────────┐
│ centos7-server.rootguru.lab                                     │
└─────────────────────────────────────────────────────────────────┘

# Host to IP mappings
/etc/hosts
┌─────────────────────────────────────────────────────────────────┐
│ 127.0.0.1   localhost localhost.localdomain                    │
│ ::1         localhost localhost.localdomain                    │
│ 192.168.1.100 centos7-server.rootguru.lab centos7-server      │
└─────────────────────────────────────────────────────────────────┘

# DNS resolution order
/etc/nsswitch.conf
┌─────────────────────────────────────────────────────────────────┐
│ hosts: files dns myhostname                                     │
└─────────────────────────────────────────────────────────────────┘

🔧 Making Network Changes Persistent:

# Method 1: Using nmcli (recommended)
sudo nmcli connection modify "System ens33" ipv4.addresses "192.168.1.100/24"
sudo nmcli connection modify "System ens33" ipv4.gateway "192.168.1.1"
sudo nmcli connection modify "System ens33" ipv4.dns "8.8.8.8,8.8.4.4"
sudo nmcli connection modify "System ens33" ipv4.method manual
sudo nmcli connection up "System ens33"

# Method 2: Edit configuration files directly
sudo vim /etc/sysconfig/network-scripts/ifcfg-ens33
sudo systemctl restart network
```

---

## 🖥️ Creating Multiple VMs for Practice

### **Setting Up a Complete Lab Environment**

#### **Lab Architecture Planning**
```
🏗️ Multi-VM Lab Design:

┌─────────────────────────────────────────────────────────────────┐
│                  rootguru Lab Environment                      │
└─────────────────────────────────────────────────────────────────┘

Virtual Network: 192.168.xxx.0/24 (VMnet8 - NAT)

┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│  CentOS7-Server │  │ CentOS7-Desktop │  │ CentOS7-Client  │
│                 │  │                 │  │                 │
│ Role: Server    │  │ Role: Admin     │  │ Role: User      │
│ RAM: 2GB        │  │ RAM: 2GB        │  │ RAM: 1GB        │
│ Disk: 20GB      │  │ Disk: 25GB      │  │ Disk: 15GB      │
│ IP: .100        │  │ IP: .101        │  │ IP: .102        │
│ Services:       │  │ GUI: GNOME      │  │ GUI: Minimal    │
│ • SSH           │  │ Tools:          │  │ Purpose:        │
│ • Web           │  │ • Firefox       │  │ • Testing       │
│ • Database      │  │ • Terminal      │  │ • Learning      │
│ • File Sharing  │  │ • Admin Tools   │  │ • Practice      │
└─────────────────┘  └─────────────────┘  └─────────────────┘

🎯 Lab Benefits:
• Practice client-server scenarios
• Test network services between VMs
• Simulate real enterprise environment
• Practice user management across systems
• Test backup and disaster recovery
```

#### **Cloning VMs for Efficiency**
```
🔄 VM Cloning Process:

Method 1: Full Clone (Recommended for Lab)
1️⃣ Shut down source VM completely
2️⃣ Right-click VM in VMware → Manage → Clone...
3️⃣ Clone Wizard:
   ┌─────────────────────────────────────────────────────────────┐
   │ Clone Source: Current state in virtual machine             │
   │ Clone Type: ● Create a full clone                          │
   │              ○ Create a linked clone                       │
   │                                                             │
   │ Full Clone Benefits:                                        │
   │ • Independent VM (no dependency on original)               │
   │ • Can move to different host                               │
   │ • Better for production-like testing                       │
   │                                                             │
   │ New VM Name: CentOS7-Desktop                               │
   │ Location: D:\VirtualMachines\VMs\CentOS7-Desktop\         │
   └─────────────────────────────────────────────────────────────┘

4️⃣ Post-Clone Configuration:
   • Change hostname
   • Assign different IP address
   • Update /etc/hosts file
   • Generate new SSH keys
   • Customize for specific role

Method 2: Template-Based Approach
1️⃣ Create base template VM with common settings
2️⃣ Install minimal CentOS + basic packages
3️⃣ Configure common settings
4️⃣ Shutdown and convert to template
5️⃣ Clone template for each specific purpose
```

#### **VM Customization After Cloning**
```
⚙️ Post-Clone Customization Checklist:

🏷️ Hostname and Network Configuration:
# Change hostname
sudo hostnamectl set-hostname centos7-desktop.rootguru.lab

# Update /etc/hosts
sudo vim /etc/hosts
# Add: 127.0.1.1 centos7-desktop.rootguru.lab centos7-desktop

# Configure static IP (optional)
sudo nmcli connection modify "System ens33" ipv4.addresses "192.168.xxx.101/24"
sudo nmcli connection up "System ens33"

🔐 Security Configuration:
# Generate new SSH host keys
sudo rm -f /etc/ssh/ssh_host_*
sudo ssh-keygen -A

# Update SSH configuration if needed
sudo systemctl restart sshd

# Create different user accounts for each VM
sudo useradd -m -G wheel desktop-admin
sudo passwd desktop-admin

🛠️ Role-Specific Customization:

For Desktop VM:
# Install desktop environment (if not done during installation)
sudo yum groupinstall -y "GNOME Desktop"
sudo systemctl set-default graphical.target

# Install additional desktop tools
sudo yum install -y firefox libreoffice gimp

For Server VM:
# Install server packages
sudo yum install -y httpd mariadb-server php

# Configure services
sudo systemctl enable httpd mariadb
sudo systemctl start httpd mariadb

For Client VM:
# Minimal configuration
sudo yum install -y git vim wget

# Remove unnecessary packages
sudo yum remove -y libreoffice-* 

📝 Documentation:
# Create VM inventory file
cat > ~/lab-inventory.txt << EOF
VM Name: CentOS7-Server
Role: Web/Database Server
IP: 192.168.xxx.100
Services: httpd, mariadb, sshd
Admin User: server-admin

VM Name: CentOS7-Desktop  
Role: Administrative Workstation
IP: 192.168.xxx.101
Services: sshd, GUI
Admin User: desktop-admin

VM Name: CentOS7-Client
Role: Test Client
IP: 192.168.xxx.102
Services: sshd
Admin User: client-admin
EOF
```

---

## 💡 Best Practices and Tips

### **Professional VM Management Guidelines**

#### **Resource Management Best Practices**
```
🎯 VM Resource Allocation Guidelines:

Memory Management:
┌─────────────────────────────────────────────────────────────────┐
│ Host RAM │ VM Allocation Strategy                                │
├──────────┼─────────────────────────────────────────────────────────┤
│ 8GB      │ 1 VM: 4GB max, 2 VMs: 2GB each                      │
│ 16GB     │ 2-3 VMs: 4GB each, or 1 large + 2 small             │
│ 32GB+    │ Multiple VMs with generous allocation                 │
└──────────┴─────────────────────────────────────────────────────────┘

Storage Best Practices:
• Allocate disk space conservatively initially
• Use thin provisioning for development VMs
• Pre-allocate for production-like testing
• Keep VMs on SSD for better performance
• Regular cleanup of snapshots

Network Planning:
• Use NAT for isolated lab environments
• Document IP address assignments
• Reserve IP ranges for different purposes:
  - .100-.110: Servers
  - .111-.120: Workstations  
  - .121-.130: Test clients
  - .131-.140: Temporary/sandbox
```

#### **Backup and Snapshot Strategy**
```
💾 VM Backup and Recovery Strategy:

Snapshot Best Practices:
┌─────────────────────────────────────────────────────────────────┐
│ Snapshot Purpose    │ When to Create                            │
├─────────────────────┼───────────────────────────────────────────┤
│ Clean Install       │ After fresh OS installation              │
│ Post-Configuration  │ After basic setup and updates            │
│ Before Changes      │ Before major configuration changes       │
│ Project Milestones  │ After completing learning modules        │
│ Backup Points       │ Weekly for active development VMs        │
└─────────────────────┴───────────────────────────────────────────┘

# Creating meaningful snapshots
VM → Snapshot → Take Snapshot
┌─────────────────────────────────────────────────────────────────┐
│ Name: Fresh_CentOS7_Install_Day2_Complete                      │
│ Description: CentOS 7 with basic configuration                 │
│ • Network configured                                            │
│ • VMware Tools installed                                        │
│ • System updated                                                │
│ • Ready for Day 3 activities                                   │
│                                                                 │
│ ✅ Snapshot the virtual machine's memory                       │
│ [Take Snapshot]                                                 │
└─────────────────────────────────────────────────────────────────┘

Backup Strategy:
• Weekly: Full VM backup for important configurations
• Daily: Snapshots during active development
• Before major changes: Always create snapshot
• Archive: Export stable configurations as OVF
```

#### **Lab Management and Organization**
```
📁 VM Organization Structure:

Directory Structure:
D:\VirtualMachines\
├── Templates\
│   ├── CentOS7-Base-Template\
│   └── Ubuntu-20-Base-Template\
├── Production-Lab\
│   ├── CentOS7-Server\
│   ├── CentOS7-Desktop\
│   └── CentOS7-Client\
├── Development\
│   ├── Test-VM-1\
│   └── Sandbox-VM\
├── Archives\
│   ├── Completed-Projects\
│   └── OVF-Exports\
└── ISOs\
    ├── CentOS-7-x86_64-DVD-2009.iso
    └── Other-ISOs\

🏷️ Naming Conventions:
VM Names: [Purpose]-[OS][Version]-[Instance]
Examples:
• Server-CentOS7-01
• Desktop-CentOS7-Admin
• Client-CentOS7-Test
• Dev-Ubuntu20-Docker

Snapshot Names: [Date]_[Purpose]_[Description]
Examples:
• 20241201_Fresh_Install_Ready_for_Config
• 20241202_Network_Configured_Updated
• 20241203_Project_Milestone_Day3_Complete

🗂️ Documentation:
# Create lab documentation
cat > ~/Lab-Documentation.md << EOF
# rootguru Linux Lab Environment

## VM Inventory
| VM Name | Purpose | IP Address | RAM | Disk | Status |
|---------|---------|------------|-----|------|--------|
| CentOS7-Server | Web/DB Server | 192.168.xxx.100 | 2GB | 20GB | Active |
| CentOS7-Desktop | Admin Station | 192.168.xxx.101 | 2GB | 25GB | Active |
| CentOS7-Client | Test Client | 192.168.xxx.102 | 1GB | 15GB | Standby |

## Network Configuration
- Network Type: NAT (VMnet8)
- Subnet: 192.168.xxx.0/24
- Gateway: 192.168.xxx.1
- DNS: 8.8.8.8, 8.8.4.4

## Access Information
- Default User: sysadmin (sudo access)
- SSH Access: ssh sysadmin@[ip-address]
- Web Services: http://192.168.xxx.100

## Snapshots
- Fresh Install: After OS installation
- Day 2 Complete: After network and basic config
- Day 3 Ready: All Day 2 topics completed
EOF
```

---

## 🏋️ Practice Exercises

### **Hands-On Lab Activities**

#### **Exercise 1: Complete VM Setup Verification**
```
🎯 Exercise 1: System Verification and Documentation

Complete these tasks to verify your installation:

Task 1.1: System Information Gathering
# Document your system configuration
echo "=== System Information Report ===" > ~/system-report.txt
echo "Date: $(date)" >> ~/system-report.txt
echo "" >> ~/system-report.txt

echo "Hostname: $(hostname -f)" >> ~/system-report.txt
echo "OS Version: $(cat /etc/redhat-release)" >> ~/system-report.txt
echo "Kernel: $(uname -r)" >> ~/system-report.txt
echo "Architecture: $(uname -m)" >> ~/system-report.txt
echo "" >> ~/system-report.txt

echo "=== Network Configuration ===" >> ~/system-report.txt
ip addr show | grep -A 2 "ens33" >> ~/system-report.txt
echo "" >> ~/system-report.txt
echo "Default Gateway: $(ip route | grep default)" >> ~/system-report.txt
echo "DNS Servers:" >> ~/system-report.txt
cat /etc/resolv.conf | grep nameserver >> ~/system-report.txt
echo "" >> ~/system-report.txt

echo "=== Storage Information ===" >> ~/system-report.txt
df -h >> ~/system-report.txt
echo "" >> ~/system-report.txt
echo "=== Memory Information ===" >> ~/system-report.txt
free -h >> ~/system-report.txt

# View your report
cat ~/system-report.txt

Task 1.2: Network Connectivity Testing
# Test various network connections
ping -c 3 127.0.0.1           # Loopback
ping -c 3 $(ip route | grep default | awk '{print $3}')  # Gateway
ping -c 3 8.8.8.8             # External IP
ping -c 3 google.com          # DNS resolution

# Test specific services
ssh localhost                  # SSH to itself (should prompt for password)
curl http://google.com         # HTTP connectivity

Task 1.3: Service Status Check
# Check important services
systemctl status NetworkManager
systemctl status sshd
systemctl status firewalld

# List all enabled services
systemctl list-unit-files --state=enabled

✅ Expected Results:
□ System report generated successfully
□ All network tests pass
□ SSH service is running
□ Can access internet (ping google.com works)
□ Hostname is properly set
□ All partitions are mounted correctly
```

#### **Exercise 2: Network Configuration Practice**
```
🌐 Exercise 2: Advanced Network Configuration

Task 2.1: Manual IP Configuration
# Current IP configuration
ip addr show ens33

# Configure static IP (replace xxx with your network)
sudo nmcli connection modify "System ens33" ipv4.addresses "192.168.xxx.150/24"
sudo nmcli connection modify "System ens33" ipv4.gateway "192.168.xxx.1"
sudo nmcli connection modify "System ens33" ipv4.dns "8.8.8.8,8.8.4.4"
sudo nmcli connection modify "System ens33" ipv4.method manual
sudo nmcli connection up "System ens33"

# Verify new configuration
ip addr show ens33
ping -c 3 google.com

# Document the change
echo "Changed to static IP: $(ip addr show ens33 | grep 'inet ' | awk '{print $2}')" >> ~/network-changes.log

Task 2.2: Hostname Configuration
# Change hostname to include your name or purpose
sudo hostnamectl set-hostname "$(whoami)-centos7.rootguru.lab"

# Update /etc/hosts
echo "127.0.1.1 $(hostname -f) $(hostname -s)" | sudo tee -a /etc/hosts

# Verify changes
hostname -f
hostnamectl

Task 2.3: Network Troubleshooting Practice
# Simulate and fix network issues

# Issue 1: Break DNS resolution
sudo cp /etc/resolv.conf /etc/resolv.conf.backup
echo "nameserver 1.2.3.4" | sudo tee /etc/resolv.conf

# Test the problem
ping -c 3 8.8.8.8           # Should work (IP)
ping -c 3 google.com        # Should fail (DNS)

# Fix the problem
sudo cp /etc/resolv.conf.backup /etc/resolv.conf

# Verify fix
ping -c 3 google.com        # Should work again

# Issue 2: Network interface down
sudo nmcli connection down "System ens33"
ping -c 3 google.com        # Should fail

# Fix it
sudo nmcli connection up "System ens33"
ping -c 3 google.com        # Should work

✅ Expected Results:
□ Successfully configured static IP
□ Hostname properly changed and persistent
□ Can identify and fix DNS issues
□ Can bring network interface up/down
□ Network troubleshooting skills demonstrated
```

#### **Exercise 3: Multi-VM Lab Setup**
```
🖥️ Exercise 3: Create Additional VMs

Task 3.1: Clone Your Current VM
1. Shutdown your current VM completely
2. Create full clone named "CentOS7-Desktop"
3. Boot both VMs
4. Configure different hostnames and IPs:

For Original VM (Server):
sudo hostnamectl set-hostname centos7-server.rootguru.lab
sudo nmcli connection modify "System ens33" ipv4.addresses "192.168.xxx.100/24"

For Cloned VM (Desktop):
sudo hostnamectl set-hostname centos7-desktop.rootguru.lab
sudo nmcli connection modify "System ens33" ipv4.addresses "192.168.xxx.101/24"

5. Update /etc/hosts on both VMs:
echo "192.168.xxx.100 centos7-server.rootguru.lab centos7-server" | sudo tee -a /etc/hosts
echo "192.168.xxx.101 centos7-desktop.rootguru.lab centos7-desktop" | sudo tee -a /etc/hosts

Task 3.2: Test Inter-VM Communication
# From Server VM:
ping -c 3 centos7-desktop
ssh sysadmin@centos7-desktop

# From Desktop VM:
ping -c 3 centos7-server
ssh sysadmin@centos7-server

Task 3.3: Configure Different Roles
Server VM - Install web server:
sudo yum install -y httpd
sudo systemctl enable httpd
sudo systemctl start httpd
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload

Desktop VM - Install development tools:
sudo yum groupinstall -y "Development Tools"
sudo yum install -y git vim code

Task 3.4: Create Lab Network Map
# Document your lab environment
cat > ~/lab-network-map.txt << EOF
=== rootguru Lab Network Map ===

Network: 192.168.xxx.0/24
Gateway: 192.168.xxx.1

VMs:
1. centos7-server.rootguru.lab (192.168.xxx.100)
   - Role: Web Server
   - Services: httpd, sshd
   - Admin: sysadmin

2. centos7-desktop.rootguru.lab (192.168.xxx.101)
   - Role: Development Workstation
   - Services: sshd, GUI
   - Admin: sysadmin

Access:
- SSH: ssh sysadmin@[hostname]
- Web: http://192.168.xxx.100
- Console: Direct VM console access

Created: $(date)
EOF

cat ~/lab-network-map.txt

✅ Expected Results:
□ Two VMs running with different hostnames
□ Different IP addresses assigned
□ VMs can ping each other by hostname
□ SSH connectivity between VMs
□ Server VM running web service
□ Desktop VM with development tools
□ Network map documented
```

---

## 🎯 Summary and Next Steps

### **Day 2 Accomplishments**

```
┌─────────────────────────────────────────────────────────────────┐
│                     Day 2 Accomplishments                      │
└─────────────────────────────────────────────────────────────────┘

✅ Lab Environment Setup:
   • VMware Workstation Pro 17 configured
   • Professional virtual lab architecture designed
   • Performance optimization applied

✅ CentOS 7 Installation Mastery:
   • Complete installation process from ISO
   • Manual partitioning with best practices
   • Software selection and customization

✅ Network Configuration Skills:
   • Static and DHCP configuration
   • Hostname management  
   • Network troubleshooting methodology
   • VMware networking concepts

✅ System Administration Foundations:
   • Post-installation configuration
   • VMware Tools installation and benefits
   • Service management basics
   • Security configuration

✅ Multi-VM Environment:
   • VM cloning and customization
   • Lab network design
   • Inter-VM communication setup
   • Role-based configuration

✅ Professional Practices:
   • Backup and snapshot strategies
   • Documentation and organization
   • Troubleshooting methodologies
   • Resource management
```

### **Preparing for Day 3**

**Topics Preview:**
- User and Group Management
- File Permissions and Ownership
- sudo Configuration and Security
- Advanced File System Operations
- System Monitoring and Logs

**Pre-Day 3 Setup:**
```bash
# Ensure your lab environment is ready:

# 1. Verify both VMs are working
ping -c 3 centos7-server
ping -c 3 centos7-desktop

# 2. Create practice users for Day 3
sudo useradd -m testuser1
sudo useradd -m testuser2
sudo passwd testuser1
sudo passwd testuser2

# 3. Create practice files and directories
mkdir -p ~/day3-practice/{files,permissions,groups}
touch ~/day3-practice/files/{file1.txt,file2.txt,file3.txt}

# 4. Install additional tools we'll use
sudo yum install -y tree htop ncdu

# 5. Create snapshot for Day 3 starting point
# VM → Snapshot → Take Snapshot
# Name: Day2_Complete_Ready_for_Day3
# Description: CentOS 7 fully configured, network setup complete
```

**Homework Practice:**
```bash
# Daily practice routine (15-20 minutes):

# Monday: VM management
# - Practice taking snapshots
# - Clone VM for testing
# - Test rollback scenarios

# Tuesday: Network configuration
# - Change IP addresses
# - Test different network modes
# - Practice troubleshooting

# Wednesday: System exploration
# - Explore /etc/sysconfig/network-scripts/
# - Practice systemctl commands
# - Monitor system resources

# Thursday: Multi-VM practice
# - Set up SSH key authentication
# - Test file sharing between VMs
# - Practice service configuration

# Friday: Documentation and cleanup
# - Update lab documentation
# - Clean up test files
# - Organize snapshots

# Weekend: Advanced exploration
# - Research LVM (Logical Volume Management)
# - Explore additional VMware features
# - Prepare questions for Day 3
```

---

## 📞 About rootguru

**🐧 Professional Linux Training** • [www.rootguru.info](http://www.rootguru.info)

*Hands-on command-line mastery to advanced system administration*

### 🎯 **Why Choose rootguru?**
- ✅ **Real-World Scenarios**: Industry-focused practical training
- ✅ **Expert Instructors**: 8 years Linux administration experience  
- ✅ **Career Support**: Job placement assistance and certification guidance
- ✅ **Flexible Learning**: Online, weekend, and corporate training available

### 📞 **Get Started Today**
- 🌐 **Website**: [www.rootguru.info](http://www.rootguru.info)
- 📧 **Email**: info@rootguru.info
- 📱 **WhatsApp**: +91-8459777100 (Training inquiries)

**© rootguru Linux Classes** | *Empowering Linux Administration Through Practical Learning* 