# Day 6: Pseudo Filesystems & System Documentation

---
**📚 Course:** rootguru Linux Classes  
**🌐 Website:** [www.rootguru.info](http://www.rootguru.info)  
**📖 Document:** Linux Fundamentals - Day 6 Pseudo Filesystems & Documentation Guide  
**🎯 Level:** Absolute Beginner  
**⏱️ Duration:** 4-5 hours  
**💻 Platform:** CentOS 7 / RHEL 7  
**👨‍🏫 Created by:** rootguru Team  

---

## 📖 Table of Contents

1. [Understanding Pseudo Filesystems](#understanding-pseudo-filesystems)
2. [The /proc Filesystem Deep Dive](#the-proc-filesystem-deep-dive)
3. [The /sys Filesystem Exploration](#the-sys-filesystem-exploration)
4. [System Information Gathering](#system-information-gathering)
5. [Linux Documentation Systems](#linux-documentation-systems)
6. [Man Pages Mastery](#man-pages-mastery)
7. [Info System and Help Commands](#info-system-and-help-commands)
8. [Online Resources and Communities](#online-resources-and-communities)
9. [Troubleshooting with Pseudo Filesystems](#troubleshooting-with-pseudo-filesystems)
10. [Interview Questions](#interview-questions)

---

## 💾 Understanding Pseudo Filesystems

### **What Are Virtual/Pseudo Filesystems?**

#### **Concept and Purpose**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Pseudo Filesystems Overview                 │
└─────────────────────────────────────────────────────────────────┘

Definition:
┌─────────────────────────────────────────────────────────────────┐
│ Pseudo filesystems are virtual filesystems that:               │
│ • Don't exist on physical storage                              │
│ • Provide interface to kernel information                      │
│ • Allow real-time access to system state                       │
│ • Present data as files and directories                        │
│ • Update dynamically as system state changes                   │
└─────────────────────────────────────────────────────────────────┘

Key Characteristics:
┌─────────────────────────────────────────────────────────────────┐
│ • Files contain live kernel data                               │
│ • No disk I/O involved                                         │
│ • Data generated on-demand                                     │
│ • Some files are read-only, others writable                    │
│ • Disappear when system shuts down                             │
│ • Recreated on every boot                                      │
└─────────────────────────────────────────────────────────────────┘

Common Pseudo Filesystems:
┌─────────────────────────────────────────────────────────────────┐
│ /proc     - Process and system information                     │
│ /sys      - Device and driver information                      │
│ /dev      - Device files                                       │
│ /run      - Runtime data                                       │
│ /tmp      - Temporary files (sometimes)                        │
│ /dev/shm  - Shared memory                                      │
└─────────────────────────────────────────────────────────────────┘
```

#### **Identifying Pseudo Filesystems**
```bash
# Commands to identify virtual filesystems

# View all mounted filesystems
mount | grep -E "(proc|sys|dev|run)"

# More detailed filesystem information
df -T | grep -E "(proc|sys|dev|run|tmp)"

# Check /proc/filesystems for supported types
cat /proc/filesystems | grep nodev

# Mount command output analysis
mount | column -t | grep -E "(proc|sys|dev)"

# Example output explanation:
# proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
# └─ Filesystem type is 'proc', mounted read-write
# └─ Security options: nosuid, nodev, noexec
```

---

## 🔍 The /proc Filesystem Deep Dive

### **Understanding Process and System Information**

#### **/proc Directory Structure**
```
┌─────────────────────────────────────────────────────────────────┐
│                    /proc Directory Layout                      │
└─────────────────────────────────────────────────────────────────┘

/proc/
├── [PID]/              # Process-specific directories
│   ├── cmdline         # Command line that started process
│   ├── environ         # Environment variables
│   ├── exe             # Link to executable file
│   ├── fd/             # File descriptors directory
│   ├── maps            # Memory mapping information
│   ├── status          # Process status summary
│   ├── stat            # Process statistics
│   └── cwd             # Current working directory link
│
├── System Information Files:
├── cpuinfo             # CPU information
├── meminfo             # Memory information
├── version             # Kernel version
├── uptime              # System uptime and idle time
├── loadavg             # Load average
├── stat                # CPU and system statistics
├── filesystems         # Supported filesystems
├── modules             # Loaded kernel modules
├── mounts              # Mounted filesystems
├── partitions          # Partition information
├── devices             # Device drivers
├── interrupts          # Interrupt statistics
├── ioports             # I/O port usage
├── iomem               # Memory usage
└── sys/                # Kernel parameters (writable)
```

#### **Practical /proc Exploration**
```bash
# Essential /proc commands and exploration

# System Information
cat /proc/version        # Kernel version and build info
cat /proc/uptime         # System uptime (seconds)
cat /proc/loadavg        # Load average (1, 5, 15 minutes)

# CPU Information
cat /proc/cpuinfo        # Detailed CPU information
grep "processor" /proc/cpuinfo | wc -l  # Count CPU cores
grep "model name" /proc/cpuinfo | head -1

# Memory Information
cat /proc/meminfo        # Comprehensive memory info
grep -E "(MemTotal|MemFree|MemAvailable)" /proc/meminfo
free -h                  # Human-readable memory summary

# Storage and Filesystems
cat /proc/filesystems    # Supported filesystem types
cat /proc/mounts        # Currently mounted filesystems
cat /proc/partitions    # Partition table
lsblk                   # Block device tree (uses /proc data)

# Network Information
cat /proc/net/dev       # Network interface statistics
cat /proc/net/route     # Routing table
cat /proc/net/arp       # ARP table

# Process Investigation
ls /proc/ | grep "^[0-9]" | head -10  # List process PIDs
cat /proc/1/cmdline     # Init process command line
cat /proc/self/status   # Current shell process status
cat /proc/$$/environ | tr '\0' '\n' | head -10  # Environment

# Kernel Parameters
ls /proc/sys/           # Kernel parameter categories
cat /proc/sys/kernel/hostname  # System hostname
cat /proc/sys/vm/swappiness    # Swap behavior setting
```

#### **/proc Process Directories Deep Dive**
```bash
# Exploring individual process information

# Pick a process to investigate (e.g., PID 1234)
PID=1234

# Basic process information
cat /proc/$PID/cmdline          # Command line
cat /proc/$PID/comm             # Command name
cat /proc/$PID/status | head -10 # Process status summary

# Process relationships
cat /proc/$PID/status | grep -E "(Pid|PPid|Tgid)"

# Memory usage
cat /proc/$PID/status | grep -E "(VmSize|VmRSS|VmData|VmStk)"
cat /proc/$PID/maps | head -10  # Memory mappings

# File descriptors
ls -la /proc/$PID/fd/           # Open file descriptors
readlink /proc/$PID/exe         # Executable path
readlink /proc/$PID/cwd         # Current working directory

# Environment and limits
cat /proc/$PID/environ | tr '\0' '\n' | grep PATH
cat /proc/$PID/limits           # Resource limits

# For your current shell
echo "My PID: $$"
cat /proc/self/cmdline          # 'self' always refers to current process
ls -la /proc/self/fd/

# Find processes by name
pgrep sshd                      # Get PIDs of sshd processes
ls /proc/$(pgrep sshd | head -1)/fd/  # Check first sshd's file descriptors
```

#### **Real-time System Monitoring with /proc**
```bash
# Create monitoring scripts using /proc

#!/bin/bash
# system_monitor.sh - Real-time system monitoring

echo "=== System Monitor ==="
echo "Time: $(date)"
echo

# CPU Load
echo "Load Average: $(cat /proc/loadavg | cut -d' ' -f1-3)"

# Memory Usage
TOTAL_MEM=$(grep MemTotal /proc/meminfo | awk '{print $2}')
FREE_MEM=$(grep MemAvailable /proc/meminfo | awk '{print $2}')
USED_MEM=$((TOTAL_MEM - FREE_MEM))
MEM_PERCENT=$((USED_MEM * 100 / TOTAL_MEM))
echo "Memory Usage: ${MEM_PERCENT}% (${USED_MEM}kB used of ${TOTAL_MEM}kB)"

# Top 5 processes by memory
echo -e "\nTop Memory Consumers:"
ps aux --sort=-%mem --no-headers | head -5 | awk '{printf "%-20s %6s %6s\n", $11, $4"%", $6"K"}'

# Network activity
echo -e "\nNetwork Interfaces:"
awk 'NR>2 {print $1, $2, $10}' /proc/net/dev | column -t

# Uptime
UPTIME_SECONDS=$(cat /proc/uptime | cut -d. -f1)
UPTIME_DAYS=$((UPTIME_SECONDS / 86400))
UPTIME_HOURS=$(((UPTIME_SECONDS % 86400) / 3600))
echo -e "\nUptime: ${UPTIME_DAYS} days, ${UPTIME_HOURS} hours"
```

---

## ⚙️ The /sys Filesystem Exploration

### **Device and Driver Information Interface**

#### **/sys Directory Structure**
```
┌─────────────────────────────────────────────────────────────────┐
│                    /sys Directory Layout                       │
└─────────────────────────────────────────────────────────────────┘

/sys/
├── block/                  # Block devices
│   ├── sda/               # SATA disk
│   │   ├── size           # Device size in sectors
│   │   ├── removable      # Is device removable?
│   │   └── queue/         # I/O queue parameters
│   └── sr0/               # CD/DVD drive
│
├── class/                  # Device classes
│   ├── net/               # Network interfaces
│   │   ├── eth0/          # Ethernet interface
│   │   └── lo/            # Loopback interface
│   ├── input/             # Input devices
│   ├── sound/             # Sound devices
│   └── tty/               # Terminal devices
│
├── devices/                # Device tree hierarchy
│   ├── pci0000:00/        # PCI bus devices
│   ├── platform/          # Platform devices
│   └── system/            # System devices
│
├── firmware/               # Firmware information
│   ├── acpi/              # ACPI tables
│   └── dmi/               # DMI/SMBIOS info
│
├── fs/                     # Filesystem information
│   ├── ext4/              # ext4 filesystem parameters
│   └── proc/              # proc filesystem parameters
│
├── kernel/                 # Kernel parameters and info
│   ├── debug/             # Debug information
│   ├── security/          # Security modules
│   └── mm/                # Memory management
│
├── module/                 # Loaded kernel modules
│   ├── e1000/             # Network driver module
│   └── ext4/              # Filesystem driver module
│
└── power/                  # Power management
    ├── state              # System sleep states
    └── disk               # Hibernation settings
```

#### **Practical /sys Exploration**
```bash
# Essential /sys commands and exploration

# Block Device Information
ls /sys/block/                      # List all block devices
cat /sys/block/sda/size             # Disk size in sectors
cat /sys/block/sda/removable        # Is disk removable? (0=no, 1=yes)
cat /sys/block/sda/queue/scheduler  # I/O scheduler

# Network Interface Information
ls /sys/class/net/                  # List network interfaces
cat /sys/class/net/eth0/address     # MAC address
cat /sys/class/net/eth0/mtu         # Maximum transmission unit
cat /sys/class/net/eth0/operstate   # Interface state (up/down)
cat /sys/class/net/eth0/speed       # Link speed (if available)

# Hardware Information
ls /sys/devices/                    # Device hierarchy
find /sys/devices -name "*intel*" -type d | head -5
cat /sys/devices/virtual/dmi/id/product_name  # System model
cat /sys/devices/virtual/dmi/id/bios_version  # BIOS version

# Power Management
cat /sys/power/state                # Available sleep states
ls /sys/devices/system/cpu/         # CPU information
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor 2>/dev/null

# Module Information
ls /sys/module/                     # Loaded modules
cat /sys/module/e1000/version 2>/dev/null     # Module version
ls /sys/module/ext4/parameters/ 2>/dev/null   # Module parameters

# Thermal Information
find /sys -name "*temp*" -type f 2>/dev/null | head -5
find /sys -name "*thermal*" -type d 2>/dev/null | head -3

# USB Devices
ls /sys/bus/usb/devices/ 2>/dev/null
find /sys/devices -name "*usb*" -type d | head -5
```

#### **Hardware Detection with /sys**
```bash
# Hardware inventory script using /sys

#!/bin/bash
# hardware_inventory.sh - System hardware detection

echo "=== Hardware Inventory ==="
echo "Generated: $(date)"
echo

# System Information
echo "=== System Information ==="
echo "Manufacturer: $(cat /sys/devices/virtual/dmi/id/sys_vendor 2>/dev/null || echo 'Unknown')"
echo "Product: $(cat /sys/devices/virtual/dmi/id/product_name 2>/dev/null || echo 'Unknown')"
echo "BIOS Version: $(cat /sys/devices/virtual/dmi/id/bios_version 2>/dev/null || echo 'Unknown')"
echo

# CPU Information
echo "=== CPU Information ==="
CPU_COUNT=$(ls /sys/devices/system/cpu/cpu[0-9]* 2>/dev/null | wc -l)
echo "CPU Cores: $CPU_COUNT"
if [ -f /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor ]; then
    echo "CPU Governor: $(cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor)"
fi
echo

# Memory Information
echo "=== Memory Information ==="
if [ -d /sys/devices/system/memory ]; then
    MEMORY_BLOCKS=$(ls /sys/devices/system/memory/memory* 2>/dev/null | wc -l)
    echo "Memory blocks: $MEMORY_BLOCKS"
fi
echo

# Storage Devices
echo "=== Storage Devices ==="
for device in /sys/block/sd* /sys/block/nvme* /sys/block/hd* 2>/dev/null; do
    if [ -d "$device" ]; then
        DEV_NAME=$(basename $device)
        SIZE_SECTORS=$(cat $device/size 2>/dev/null)
        SIZE_GB=$(($SIZE_SECTORS * 512 / 1000000000))
        REMOVABLE=$(cat $device/removable 2>/dev/null)
        echo "Device: $DEV_NAME, Size: ${SIZE_GB}GB, Removable: $REMOVABLE"
    fi
done
echo

# Network Interfaces
echo "=== Network Interfaces ==="
for interface in /sys/class/net/*; do
    if [ -d "$interface" ]; then
        IFACE=$(basename $interface)
        if [ "$IFACE" != "lo" ]; then
            MAC=$(cat $interface/address 2>/dev/null)
            STATE=$(cat $interface/operstate 2>/dev/null)
            echo "Interface: $IFACE, MAC: $MAC, State: $STATE"
        fi
    fi
done
```

---

## 📊 System Information Gathering

### **Comprehensive System Analysis**

#### **Hardware Information Commands**
```bash
# Comprehensive hardware detection commands

# CPU Information
lscpu                           # Detailed CPU information
cat /proc/cpuinfo | grep "model name" | head -1
nproc                          # Number of processing units

# Memory Information
free -h                        # Memory usage summary
dmidecode -t memory 2>/dev/null | grep -A5 "Memory Device" | head -20
cat /proc/meminfo | grep -E "(MemTotal|SwapTotal)"

# Storage Information
lsblk                          # Block device tree
fdisk -l 2>/dev/null | head -20 # Partition tables
df -h                          # Mounted filesystem usage

# Network Information
ip addr show                   # Network interfaces and IPs
ip route show                  # Routing table
lspci | grep -i network        # PCI network devices

# USB Information
lsusb                          # USB devices
lsusb -v | head -20           # Verbose USB information

# PCI Information
lspci                          # PCI devices
lspci -v | head -20           # Verbose PCI information

# Hardware Summary
dmidecode -t system 2>/dev/null # System information
dmidecode -t bios 2>/dev/null   # BIOS information
```

#### **System Status Monitoring**
```bash
# System status and performance monitoring

# Current system load
uptime
cat /proc/loadavg

# Process information
ps aux | head -10              # Process list
top -b -n1 | head -20         # Process snapshot
pstree                        # Process tree

# Memory usage analysis
cat /proc/meminfo | head -10
vmstat 1 5                    # Virtual memory statistics
sar -r 1 5 2>/dev/null        # Memory utilization over time

# Disk I/O
iostat 1 5 2>/dev/null        # I/O statistics
iotop -b -n1 2>/dev/null | head -10  # I/O by process

# Network activity
netstat -i                    # Interface statistics
ss -tuln                      # Socket statistics
iftop -t -s 10 2>/dev/null    # Network traffic by interface

# System logs
journalctl -n 20              # Recent system messages
dmesg | tail -20              # Kernel messages
```

---

## 📚 Linux Documentation Systems

### **Understanding Built-in Help Systems**

#### **Documentation Hierarchy**
```
┌─────────────────────────────────────────────────────────────────┐
│                  Linux Documentation Levels                    │
└─────────────────────────────────────────────────────────────────┘

Level 1: Quick Help
┌─────────────────────────────────────────────────────────────────┐
│ command --help        # Brief usage summary                    │
│ command -h            # Short help option                      │
│ type command          # Command type and location              │
│ which command         # Command location                       │
│ whatis command        # One-line description                   │
└─────────────────────────────────────────────────────────────────┘

Level 2: Manual Pages
┌─────────────────────────────────────────────────────────────────┐
│ man command           # Detailed manual page                   │
│ man -k keyword        # Search manual pages                    │
│ apropos keyword       # Same as man -k                         │
│ man -f command        # Same as whatis                         │
└─────────────────────────────────────────────────────────────────┘

Level 3: Info System
┌─────────────────────────────────────────────────────────────────┐
│ info command          # GNU info documentation                 │
│ info --help           # Info system help                       │
│ pinfo command         # Enhanced info reader                   │
└─────────────────────────────────────────────────────────────────┘

Level 4: Documentation Files
┌─────────────────────────────────────────────────────────────────┐
│ /usr/share/doc/       # Package documentation                  │
│ /usr/local/share/doc/ # Local documentation                    │
│ README files          # Package-specific information           │
│ HOWTOs and guides     # Detailed procedures                    │
└─────────────────────────────────────────────────────────────────┘
```

#### **Documentation Location Map**
```bash
# Finding documentation on your system

# System documentation directories
ls /usr/share/doc/ | head -10
ls /usr/share/man/
ls /usr/share/info/

# Package-specific documentation
rpm -ql bash | grep doc
find /usr/share/doc -name "*bash*" -type d

# Manual page locations
manpath                        # Show manual page search path
man -w ls                      # Show location of ls manual page

# Info documentation
ls /usr/share/info/ | head -10

# Help and examples
ls /usr/share/doc/*/examples/ 2>/dev/null | head -5
ls /usr/share/doc/*/README* 2>/dev/null | head -5

# Online manual pages (if available)
curl -s "https://linux.die.net/man/1/ls" | grep -A5 "<title>" 2>/dev/null
```

---

## 📖 Man Pages Mastery

### **Mastering the Manual System**

#### **Man Page Sections**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Manual Page Sections                        │
└─────────────────────────────────────────────────────────────────┘

Section 1: User Commands
┌─────────────────────────────────────────────────────────────────┐
│ Commands that any user can execute                              │
│ Examples: ls, cp, mv, grep, find, ssh                          │
│ Usage: man 1 ls  or  man ls                                    │
└─────────────────────────────────────────────────────────────────┘

Section 2: System Calls
┌─────────────────────────────────────────────────────────────────┐
│ Functions provided by the kernel                                │
│ Examples: open, read, write, fork, exec                        │
│ Usage: man 2 open                                              │
└─────────────────────────────────────────────────────────────────┘

Section 3: Library Functions
┌─────────────────────────────────────────────────────────────────┐
│ Functions provided by program libraries                         │
│ Examples: printf, malloc, strlen                               │
│ Usage: man 3 printf                                            │
└─────────────────────────────────────────────────────────────────┘

Section 4: Device Files
┌─────────────────────────────────────────────────────────────────┐
│ Device files in /dev                                           │
│ Examples: null, random, tty                                    │
│ Usage: man 4 null                                              │
└─────────────────────────────────────────────────────────────────┘

Section 5: File Formats
┌─────────────────────────────────────────────────────────────────┐
│ Configuration files and file formats                           │
│ Examples: passwd, fstab, hosts                                 │
│ Usage: man 5 passwd                                            │
└─────────────────────────────────────────────────────────────────┘

Section 8: System Administration
┌─────────────────────────────────────────────────────────────────┐
│ Commands for system administrators                              │
│ Examples: mount, useradd, systemctl                           │
│ Usage: man 8 mount                                             │
└─────────────────────────────────────────────────────────────────┘
```

#### **Advanced Man Page Usage**
```bash
# Advanced manual page commands

# Section-specific access
man 1 passwd                   # User command
man 5 passwd                   # File format
man 8 passwd                   # Admin command (if exists)

# Search manual pages
man -k password                # Search for keyword
apropos network                # Find network-related commands
man -K "regular expression"    # Search manual page content

# Manual page information
whatis ls                      # Brief description
man -f cp                      # Same as whatis
man -w ls                      # Show manual page file location

# Manual page navigation
# Inside man pages:
# h          - Help
# q          - Quit
# Space      - Next page
# b          - Previous page
# /pattern   - Search forward
# ?pattern   - Search backward
# n          - Next search result
# N          - Previous search result
# g          - Go to beginning
# G          - Go to end

# Converting man pages
man -t ls > ls_manual.ps       # PostScript format
man ls | col -b > ls_manual.txt # Plain text

# Multiple manual pages
man bash | grep -A10 "SHELL BUILTIN COMMANDS"
```

#### **Creating Your Own Man Page Quick Reference**
```bash
# Create a personal command reference

#!/bin/bash
# create_command_reference.sh - Build personal command cheat sheet

echo "=== Personal Linux Command Reference ==="
echo "Generated: $(date)"
echo

COMMANDS="ls cd pwd cp mv rm mkdir rmdir find grep sed awk sort uniq wc head tail cat less more chmod chown ps top kill jobs bg fg ssh scp rsync tar gzip systemctl"

for cmd in $COMMANDS; do
    echo "=== $cmd ==="
    whatis $cmd 2>/dev/null || echo "No description available"
    echo "Location: $(which $cmd 2>/dev/null || echo 'Not found')"
    echo "Usage: $(man $cmd 2>/dev/null | grep -A1 "^SYNOPSIS" | tail -1 | sed 's/^[ \t]*//' || echo 'See man page')"
    echo
done

echo "=== Manual Page Sections ==="
echo "1. User Commands"
echo "2. System Calls"  
echo "3. Library Functions"
echo "4. Device Files"
echo "5. File Formats"
echo "8. System Administration"
echo
echo "Usage: man [section] command"
echo "Search: man -k keyword, apropos keyword"
```

---

## ℹ️ Info System and Help Commands

### **GNU Info Documentation System**

#### **Info System Navigation**
```
┌─────────────────────────────────────────────────────────────────┐
│                    GNU Info System                             │
└─────────────────────────────────────────────────────────────────┘

Info vs Man Pages:
┌─────────────────────────────────────────────────────────────────┐
│ Man Pages:                    │ Info Pages:                    │
│ • Single page format          │ • Hyperlinked documents        │
│ • Traditional Unix style      │ • GNU project standard         │
│ • Concise reference           │ • Detailed tutorials           │
│ • Wide compatibility          │ • Cross-referenced topics      │
└─────────────────────────────────────────────────────────────────┘

Info Navigation Keys:
┌─────────────────────────────────────────────────────────────────┐
│ Space     - Scroll down                                         │
│ Backspace - Scroll up                                           │
│ n         - Next node                                           │
│ p         - Previous node                                       │
│ u         - Up to parent node                                   │
│ l         - Last visited node                                   │
│ d         - Directory (top level)                               │
│ q         - Quit                                                │
│ ?         - Help                                                │
│ s         - Search                                              │
│ Tab       - Next cross-reference                                │
│ Enter     - Follow cross-reference                              │
└─────────────────────────────────────────────────────────────────┘
```

#### **Practical Info Usage**
```bash
# GNU Info system commands

# Basic info usage
info                           # Top-level info directory
info bash                      # Bash manual in info format
info coreutils                 # GNU core utilities documentation
info grep                      # grep documentation

# Info command options
info --help                    # Info system help
info --version                 # Info version
info -f filename               # Read specific info file
info -n nodename               # Start at specific node

# Alternative info readers
pinfo bash 2>/dev/null         # Enhanced info reader (if available)

# Converting info to other formats
info --output=bash_manual.txt bash 2>/dev/null

# Check available info documents
ls /usr/share/info/ | grep ".info" | head -10

# Help command variations
help                           # Shell builtin help (in bash)
help cd                        # Help for cd builtin
type -a help                   # Show help command type

# Command-specific help
ls --help | head -10
grep --help | head -10
find --help | head -10

# Getting help about help
man help
info help
help help
```

---

## 🌐 Online Resources and Communities

### **External Documentation and Support**

#### **Essential Online Resources**
```
┌─────────────────────────────────────────────────────────────────┐
│                  Essential Linux Resources                     │
└─────────────────────────────────────────────────────────────────┘

Official Documentation:
┌─────────────────────────────────────────────────────────────────┐
│ • The Linux Documentation Project (TLDP)                       │
│   └─ https://tldp.org/                                         │
│ • Kernel.org Documentation                                     │
│   └─ https://www.kernel.org/doc/                               │
│ • GNU Project Documentation                                    │
│   └─ https://www.gnu.org/manual/                               │
└─────────────────────────────────────────────────────────────────┘

Distribution-Specific:
┌─────────────────────────────────────────────────────────────────┐
│ • Red Hat Documentation                                        │
│   └─ https://access.redhat.com/documentation/                  │
│ • CentOS Documentation                                         │
│   └─ https://wiki.centos.org/                                  │
│ • Ubuntu Documentation                                         │
│   └─ https://help.ubuntu.com/                                  │
│ • Arch Linux Wiki (excellent for all distributions)           │
│   └─ https://wiki.archlinux.org/                               │
└─────────────────────────────────────────────────────────────────┘

Reference Sites:
┌─────────────────────────────────────────────────────────────────┐
│ • Man7.org (online manual pages)                               │
│   └─ https://man7.org/linux/man-pages/                         │
│ • Linux.die.net (command references)                           │
│   └─ https://linux.die.net/                                    │
│ • ExplainShell (command explanation)                           │
│   └─ https://explainshell.com/                                 │
└─────────────────────────────────────────────────────────────────┘

Communities:
┌─────────────────────────────────────────────────────────────────┐
│ • Stack Overflow (programming questions)                       │
│ • Unix & Linux Stack Exchange (system administration)          │
│ • Reddit: r/linux, r/linuxadmin, r/sysadmin                   │
│ • LinuxQuestions.org (beginner-friendly)                       │
│ • IRC channels: #linux on freenode                            │
└─────────────────────────────────────────────────────────────────┘
```

#### **Finding Help Effectively**
```bash
# Strategies for finding help online

# Local command exploration first
man command_name
command_name --help
info command_name
which command_name
type command_name

# Search strategies
# 1. Include Linux distribution in search
#    "centos 7 configure network interface"
# 2. Include error messages exactly
#    "bash: command not found: xyz"
# 3. Include version numbers
#    "systemd 219 service failed"

# Building a search query
ERROR_MSG="Permission denied"
COMMAND="chmod"
DISTRO="centos 7"
echo "Search query: '$DISTRO $COMMAND $ERROR_MSG'"

# Document your solutions
mkdir ~/linux_solutions
echo "# $(date): Fixed permission issue" >> ~/linux_solutions/permissions.md
echo "Problem: $ERROR_MSG" >> ~/linux_solutions/permissions.md
echo "Solution: chmod +x filename" >> ~/linux_solutions/permissions.md
echo "Source: man chmod" >> ~/linux_solutions/permissions.md
```

---

## 🔧 Troubleshooting with Pseudo Filesystems

### **Using /proc and /sys for Problem Solving**

#### **Common Troubleshooting Scenarios**
```bash
# Troubleshooting with /proc and /sys

# Scenario 1: High CPU usage
echo "=== CPU Troubleshooting ==="
cat /proc/loadavg                    # Check load average
ps aux --sort=-%cpu | head -10       # Top CPU consumers
cat /proc/stat | grep cpu            # CPU statistics
cat /proc/interrupts | head -10      # Interrupt activity

# Scenario 2: Memory issues
echo -e "\n=== Memory Troubleshooting ==="
cat /proc/meminfo | grep -E "(MemTotal|MemFree|MemAvailable|SwapTotal|SwapFree)"
cat /proc/sys/vm/swappiness          # Swap behavior
ps aux --sort=-%mem | head -10       # Top memory consumers

# Scenario 3: Network connectivity issues
echo -e "\n=== Network Troubleshooting ==="
cat /proc/net/dev                    # Interface statistics
cat /sys/class/net/eth0/operstate    # Interface state
cat /sys/class/net/eth0/carrier      # Physical link status
cat /proc/net/route                  # Routing table

# Scenario 4: Disk I/O problems
echo -e "\n=== Storage Troubleshooting ==="
cat /proc/diskstats                  # Disk statistics
ls /sys/block/                       # Available block devices
cat /sys/block/sda/queue/scheduler   # I/O scheduler
cat /proc/mounts | grep sda          # Mounted filesystems

# Scenario 5: Process debugging
echo -e "\n=== Process Troubleshooting ==="
PROCESS_NAME="httpd"
PIDS=$(pgrep $PROCESS_NAME)
for pid in $PIDS; do
    echo "Process $pid:"
    cat /proc/$pid/status | grep -E "(State|VmSize|VmRSS)"
    ls /proc/$pid/fd/ | wc -l | awk '{print "Open files:", $1}'
done
```

#### **System Health Check Script**
```bash
#!/bin/bash
# system_health_check.sh - Comprehensive system health check

echo "=== System Health Check ==="
echo "Timestamp: $(date)"
echo "Hostname: $(hostname)"
echo

# Check system uptime and load
echo "=== System Load ==="
UPTIME_DATA=$(cat /proc/uptime)
UPTIME_SECONDS=$(echo $UPTIME_DATA | cut -d. -f1)
UPTIME_DAYS=$((UPTIME_SECONDS / 86400))
UPTIME_HOURS=$(((UPTIME_SECONDS % 86400) / 3600))
echo "Uptime: ${UPTIME_DAYS} days, ${UPTIME_HOURS} hours"

LOAD_AVG=$(cat /proc/loadavg | cut -d' ' -f1-3)
echo "Load Average: $LOAD_AVG"

# Check memory usage
echo -e "\n=== Memory Status ==="
TOTAL_MEM=$(grep MemTotal /proc/meminfo | awk '{print $2}')
FREE_MEM=$(grep MemAvailable /proc/meminfo | awk '{print $2}')
USED_MEM=$((TOTAL_MEM - FREE_MEM))
MEM_PERCENT=$((USED_MEM * 100 / TOTAL_MEM))
echo "Memory Usage: ${MEM_PERCENT}% ($(($USED_MEM/1024))MB used of $(($TOTAL_MEM/1024))MB)"

SWAP_TOTAL=$(grep SwapTotal /proc/meminfo | awk '{print $2}')
SWAP_FREE=$(grep SwapFree /proc/meminfo | awk '{print $2}')
if [ $SWAP_TOTAL -gt 0 ]; then
    SWAP_USED=$((SWAP_TOTAL - SWAP_FREE))
    SWAP_PERCENT=$((SWAP_USED * 100 / SWAP_TOTAL))
    echo "Swap Usage: ${SWAP_PERCENT}% ($(($SWAP_USED/1024))MB used of $(($SWAP_TOTAL/1024))MB)"
fi

# Check disk usage
echo -e "\n=== Storage Status ==="
df -h | grep -E "(Filesystem|/dev/)" | head -5

# Check network interfaces
echo -e "\n=== Network Status ==="
for interface in /sys/class/net/*; do
    if [ -d "$interface" ]; then
        IFACE=$(basename $interface)
        if [ "$IFACE" != "lo" ]; then
            STATE=$(cat $interface/operstate 2>/dev/null)
            echo "Interface $IFACE: $STATE"
        fi
    fi
done

# Check for common issues
echo -e "\n=== Potential Issues ==="
if [ $MEM_PERCENT -gt 90 ]; then
    echo "WARNING: High memory usage ($MEM_PERCENT%)"
fi

if [ -n "$SWAP_PERCENT" ] && [ $SWAP_PERCENT -gt 50 ]; then
    echo "WARNING: High swap usage ($SWAP_PERCENT%)"
fi

LOAD_1MIN=$(echo $LOAD_AVG | cut -d' ' -f1)
CPU_COUNT=$(nproc)
if (( $(echo "$LOAD_1MIN > $CPU_COUNT" | bc -l) )); then
    echo "WARNING: High load average ($LOAD_1MIN for $CPU_COUNT CPUs)"
fi

echo -e "\n=== Check Complete ==="
```

---

## 🎯 Interview Questions

### **Pseudo Filesystems and Documentation Interview Questions**

#### **Question 1: /proc vs /sys**
```
Q: Explain the difference between /proc and /sys filesystems. When would you 
   use each one?

Expected Answer:
- /proc: Process and system information, general system stats
- /sys: Device and driver information, hardware-focused
- /proc examples: /proc/cpuinfo, /proc/meminfo, /proc/[PID]/
- /sys examples: /sys/class/net/, /sys/block/, /sys/devices/
- Both are virtual filesystems with live kernel data
```

#### **Question 2: Process Investigation**
```
Q: How would you investigate a process that's consuming high memory using 
   the /proc filesystem?

Expected Answer:
- Find PID: ps aux | grep process_name or pgrep process_name
- Memory usage: /proc/[PID]/status (VmSize, VmRSS, VmData)
- Memory mapping: /proc/[PID]/maps
- Open files: /proc/[PID]/fd/
- Command line: /proc/[PID]/cmdline
- Environment: /proc/[PID]/environ
```

#### **Question 3: Man Page Sections**
```
Q: What's the difference between 'man 1 passwd' and 'man 5 passwd'?

Expected Answer:
- man 1 passwd: User command for changing passwords
- man 5 passwd: File format of /etc/passwd file
- Section 1: User commands
- Section 5: File formats and configuration files
- Same name, different documentation for different purposes
```

#### **Question 4: System Monitoring**
```
Q: Using /proc filesystem, how would you monitor system load and identify 
   performance bottlenecks?

Expected Answer:
- /proc/loadavg: Load average (1, 5, 15 minutes)
- /proc/stat: CPU utilization statistics
- /proc/meminfo: Memory usage and availability
- /proc/diskstats: Disk I/O statistics
- /proc/net/dev: Network interface statistics
- Compare values over time to identify trends
```

---

## 🎯 Summary and Next Steps

### **Day 6 Accomplishments**

✅ **Pseudo Filesystems and Documentation Mastery Achieved:**
- Virtual filesystem concepts and purposes
- /proc filesystem navigation and analysis
- /sys filesystem hardware investigation
- System information gathering techniques
- Linux documentation system hierarchy
- Man page section understanding and navigation
- Info system usage and navigation
- Online resource identification and usage
- Troubleshooting with pseudo filesystems
- System health monitoring scripts

### **Key Takeaways:**
```
Essential Documentation Concepts:
┌─────────────────────────────────────────────────────────────────┐
│ • /proc provides live system and process information            │
│ • /sys exposes hardware and device driver data                 │
│ • Man pages are organized in numbered sections                 │
│ • Multiple documentation layers provide different detail levels │
│ • Online communities are valuable for complex problems         │
│ • Pseudo filesystems are powerful troubleshooting tools        │
└─────────────────────────────────────────────────────────────────┘
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