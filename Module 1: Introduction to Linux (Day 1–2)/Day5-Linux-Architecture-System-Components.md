# Day 5: Linux Architecture & System Components

---
**📚 Course:** rootguru Linux Classes  
**🌐 Website:** [www.rootguru.info](http://www.rootguru.info)  
**📖 Document:** Linux Fundamentals - Day 5 Architecture & Components Guide  
**🎯 Level:** Absolute Beginner  
**⏱️ Duration:** 4-5 hours  
**💻 Platform:** CentOS 7 / RHEL 7  
**👨‍🏫 Created by:** rootguru Team  

---

## 📖 Table of Contents

1. [Complete Linux System Architecture](#complete-linux-system-architecture)
2. [Kernel vs User Space Deep Dive](#kernel-vs-user-space-deep-dive)
3. [Linux Kernel Components](#linux-kernel-components)
4. [Init Systems Evolution](#init-systems-evolution)
5. [System Libraries and APIs](#system-libraries-and-apis)
6. [Process Management Architecture](#process-management-architecture)
7. [Monolithic vs Microkernel](#monolithic-vs-microkernel)
8. [Device Drivers and Hardware](#device-drivers-and-hardware)
9. [Memory Management](#memory-management)
10. [Interview Questions](#interview-questions)

---

## 🏗️ Complete Linux System Architecture

### **Understanding the Full System Stack**

#### **Linux System Architecture Layers**
```
┌─────────────────────────────────────────────────────────────────┐
│                  Complete Linux Architecture                   │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                      User Applications                         │ ← Layer 7
│ (Web browsers, Text editors, Games, Office suites, etc.)       │
├─────────────────────────────────────────────────────────────────┤
│                      Shell & Utilities                         │ ← Layer 6
│ (bash, zsh, coreutils: ls, cp, mv, grep, etc.)                │
├─────────────────────────────────────────────────────────────────┤
│                    Desktop Environment                         │ ← Layer 5
│ (GNOME, KDE, XFCE - Optional GUI layer)                       │
├─────────────────────────────────────────────────────────────────┤
│                    System Libraries                            │ ← Layer 4
│ (glibc, libssl, libxml, shared libraries, frameworks)         │
├─────────────────────────────────────────────────────────────────┤
│                      System Calls                              │ ← Layer 3
│ (API between user space and kernel space)                     │
├═════════════════════════════════════════════════════════════════┤ ← Kernel Boundary
│                      Linux Kernel                              │ ← Layer 2
│ (Process mgmt, Memory mgmt, Filesystem, Network, Devices)     │
├─────────────────────────────────────────────────────────────────┤
│                       Hardware                                 │ ← Layer 1
│ (CPU, RAM, Storage, Network interfaces, Peripherals)          │
└─────────────────────────────────────────────────────────────────┘

Information Flow:
User Request → Shell → System Call → Kernel → Hardware → Response
```

#### **Component Interaction Example**
```
Example: User runs "ls /home" command
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  1. User types: ls /home                                        │
│  2. Shell (bash) parses command                                 │
│  3. Shell executes /bin/ls program                             │
│  4. ls program makes system calls:                             │
│     • opendir("/home")    - Open directory                     │
│     • readdir()           - Read directory entries             │
│     • stat()              - Get file information               │
│     • write()             - Output to terminal                 │
│  5. Kernel processes system calls:                             │
│     • Filesystem driver reads disk                             │
│     • Memory manager allocates buffers                         │
│     • Terminal driver displays output                          │
│  6. Hardware executes operations:                              │
│     • Disk controller reads data                               │
│     • Video card displays text                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔐 Kernel vs User Space Deep Dive

### **Understanding the Critical Boundary**

#### **Kernel Space Characteristics**
```
┌─────────────────────────────────────────────────────────────────┐
│                       Kernel Space                             │
└─────────────────────────────────────────────────────────────────┘

Privileges:
┌─────────────────────────────────────────────────────────────────┐
│ • Direct hardware access                                       │
│ • Execute privileged instructions                              │
│ • Manage system resources                                      │
│ • Control memory protection                                    │
│ • Handle interrupts and exceptions                             │
│ • No memory protection (can crash system)                     │
└─────────────────────────────────────────────────────────────────┘

Contents:
┌─────────────────────────────────────────────────────────────────┐
│ • Linux kernel core                                            │
│ • Device drivers                                               │
│ • Kernel modules                                               │
│ • System call handlers                                         │
│ • Interrupt handlers                                           │
│ • Memory management code                                       │
└─────────────────────────────────────────────────────────────────┘

Memory Layout:
┌─────────────────────────────────────────────────────────────────┐
│                    Virtual Memory Map                          │
│ 0xFFFFFFFF ┌─────────────────────────────────────────────────┐ │
│            │           Kernel Space                          │ │
│            │        (1GB on 32-bit systems)                 │ │
│ 0xC0000000 ├─────────────────────────────────────────────────┤ │
│            │                                                 │ │
│            │           User Space                            │ │
│            │        (3GB on 32-bit systems)                 │ │
│            │                                                 │ │
│ 0x00000000 └─────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

#### **User Space Characteristics**
```
┌─────────────────────────────────────────────────────────────────┐
│                        User Space                              │
└─────────────────────────────────────────────────────────────────┘

Restrictions:
┌─────────────────────────────────────────────────────────────────┐
│ • No direct hardware access                                    │
│ • Cannot execute privileged instructions                       │
│ • Memory protection enforced                                   │
│ • Must use system calls for kernel services                   │
│ • Process isolation maintained                                 │
│ • Crashes contained to single process                          │
└─────────────────────────────────────────────────────────────────┘

Contents:
┌─────────────────────────────────────────────────────────────────┐
│ • Application programs                                          │
│ • System utilities                                             │
│ • Shared libraries                                             │
│ • Shell and command interpreters                              │
│ • Desktop environments                                         │
│ • User data and configurations                                │
└─────────────────────────────────────────────────────────────────┘

Protection Mechanisms:
┌─────────────────────────────────────────────────────────────────┐
│ • Virtual memory per process                                   │
│ • CPU privilege levels (Ring 0=kernel, Ring 3=user)           │
│ • Memory access permissions (read/write/execute)               │
│ • System call interface (controlled kernel access)             │
│ • Process accounting and limits                                │
└─────────────────────────────────────────────────────────────────┘
```

#### **System Call Interface**
```bash
# Practical Examples: Observing System Calls

# Use strace to see system calls made by commands
strace ls /home

# Common system calls you'll see:
# execve() - Execute program
# openat() - Open file/directory  
# read()   - Read data
# write()  - Write data
# close()  - Close file descriptor
# exit()   - Terminate process

# Trace specific system calls
strace -e trace=open,openat,read ls /etc

# Count system calls
strace -c ls /home

# Follow forked processes
strace -f bash -c "ls | wc -l"

# Output to file for analysis
strace -o ls_trace.txt ls /home
less ls_trace.txt
```

---

## 🧠 Linux Kernel Components

### **Understanding Kernel Subsystems**

#### **Major Kernel Subsystems**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Linux Kernel Components                     │
└─────────────────────────────────────────────────────────────────┘

Process Management:
┌─────────────────────────────────────────────────────────────────┐
│ • Process scheduler (CFS - Completely Fair Scheduler)          │
│ • Process creation and termination                             │
│ • Inter-process communication (IPC)                            │
│ • Signal handling                                              │
│ • Process accounting and limits                                │
│                                                                 │
│ Key Files: kernel/sched/, kernel/fork.c, kernel/signal.c       │
└─────────────────────────────────────────────────────────────────┘

Memory Management:
┌─────────────────────────────────────────────────────────────────┐
│ • Virtual memory management                                     │
│ • Page allocation and deallocation                             │
│ • Memory mapping (mmap)                                        │
│ • Swap management                                              │
│ • Memory protection and segmentation                           │
│                                                                 │
│ Key Files: mm/, arch/*/mm/                                     │
└─────────────────────────────────────────────────────────────────┘

Filesystem Layer:
┌─────────────────────────────────────────────────────────────────┐
│ • Virtual File System (VFS) interface                          │
│ • Individual filesystem drivers (ext4, xfs, btrfs)            │
│ • Block device layer                                           │
│ • Buffer cache management                                      │
│ • File locking and security                                    │
│                                                                 │
│ Key Files: fs/, include/linux/fs.h                            │
└─────────────────────────────────────────────────────────────────┘

Network Stack:
┌─────────────────────────────────────────────────────────────────┐
│ • TCP/IP protocol implementation                               │
│ • Socket interface                                             │
│ • Network device drivers                                       │
│ • Firewall and packet filtering (netfilter)                   │
│ • Network namespaces                                           │
│                                                                 │
│ Key Files: net/, drivers/net/                                  │
└─────────────────────────────────────────────────────────────────┘

Device Drivers:
┌─────────────────────────────────────────────────────────────────┐
│ • Character device drivers                                      │
│ • Block device drivers                                         │
│ • Network device drivers                                       │
│ • USB, PCI, and other bus drivers                             │
│ • Hardware abstraction layer                                   │
│                                                                 │
│ Key Files: drivers/, arch/*/                                   │
└─────────────────────────────────────────────────────────────────┘
```

#### **Kernel Information Commands**
```bash
# Exploring kernel information

# Check kernel version and compile info
uname -a
cat /proc/version

# View kernel configuration (if available)
cat /proc/config.gz | gunzip | less
# Or check boot directory
ls /boot/config-*

# View kernel command line parameters
cat /proc/cmdline

# Check loaded kernel modules
lsmod

# Get information about specific module
modinfo ext4
modinfo e1000  # network driver

# View kernel messages
dmesg | less
dmesg | tail -20

# Check kernel memory usage
cat /proc/meminfo
cat /proc/slabinfo

# View interrupts and their handlers
cat /proc/interrupts

# Check CPU information from kernel perspective
cat /proc/cpuinfo
```

---

## 🔄 Init Systems Evolution

### **Understanding System Initialization**

#### **Init System Comparison**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Init System Evolution                       │
└─────────────────────────────────────────────────────────────────┘

SysV Init (Traditional):
┌─────────────────────────────────────────────────────────────────┐
│ Design: Sequential startup scripts                              │
│ Config: /etc/init.d/ scripts, /etc/rc*.d/ links               │
│ Control: service command, chkconfig                            │
│ Runlevels: 0-6 (single user, multi-user, graphical, etc.)     │
│                                                                 │
│ Pros:                                                           │
│ • Simple and well understood                                   │
│ • Portable across Unix systems                                │
│ • Easy to debug and customize                                  │
│                                                                 │
│ Cons:                                                           │
│ • Slow sequential startup                                      │
│ • No dependency management                                     │
│ • Shell script overhead                                        │
│ • Limited process supervision                                  │
└─────────────────────────────────────────────────────────────────┘

systemd (Modern):
┌─────────────────────────────────────────────────────────────────┐
│ Design: Parallel startup with dependencies                     │
│ Config: Unit files (.service, .target, .socket, etc.)        │
│ Control: systemctl command                                     │
│ Targets: Equivalent to runlevels (multi-user.target, etc.)    │
│                                                                 │
│ Pros:                                                           │
│ • Fast parallel startup                                        │
│ • Sophisticated dependency management                          │
│ • Built-in logging (journald)                                 │
│ • Socket and D-Bus activation                                  │
│ • Process supervision and restart                              │
│                                                                 │
│ Cons:                                                           │
│ • Complex and controversial                                    │
│ • Large codebase                                               │
│ • Linux-specific                                               │
│ • Learning curve for administrators                            │
└─────────────────────────────────────────────────────────────────┘
```

#### **systemd Architecture**
```
┌─────────────────────────────────────────────────────────────────┐
│                    systemd Architecture                        │
└─────────────────────────────────────────────────────────────────┘

Core Components:
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  systemd (PID 1)                                               │
│  ├── Unit Management                                           │
│  │   ├── Services (.service)                                  │
│  │   ├── Targets (.target) - groups of units                 │
│  │   ├── Sockets (.socket) - network/IPC                     │
│  │   ├── Timers (.timer) - scheduled tasks                   │
│  │   └── Mounts (.mount) - filesystem mounts                 │
│  │                                                             │
│  ├── Process Supervision                                       │
│  │   ├── Start/stop services                                  │
│  │   ├── Monitor and restart                                  │
│  │   └── Resource limits (cgroups)                           │
│  │                                                             │
│  ├── Dependency Engine                                         │
│  │   ├── Requires= (hard dependency)                          │
│  │   ├── Wants= (soft dependency)                             │
│  │   ├── After= (ordering)                                    │
│  │   └── Before= (ordering)                                   │
│  │                                                             │
│  └── Logging Integration                                       │
│      ├── journald (log daemon)                                │
│      ├── Structured logging                                   │
│      └── Log correlation                                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### **Practical systemd Commands**
```bash
# Essential systemd commands

# Check systemd version and features
systemctl --version

# View system state
systemctl status

# List all units
systemctl list-units

# List all services
systemctl list-units --type=service

# Check specific service
systemctl status sshd
systemctl status NetworkManager

# Start/stop/restart services
sudo systemctl start httpd
sudo systemctl stop httpd
sudo systemctl restart httpd
sudo systemctl reload httpd

# Enable/disable services (boot time)
sudo systemctl enable httpd
sudo systemctl disable httpd
sudo systemctl is-enabled httpd

# View service configuration
systemctl cat httpd
systemctl show httpd

# Check dependencies
systemctl list-dependencies httpd
systemctl list-dependencies graphical.target

# View current target (runlevel equivalent)
systemctl get-default
systemctl list-units --type=target

# Change target
sudo systemctl isolate multi-user.target
sudo systemctl set-default graphical.target

# Analyze boot time
systemd-analyze
systemd-analyze blame
systemd-analyze critical-chain
```

---

## 📚 System Libraries and APIs

### **Understanding the Library Layer**

#### **GNU C Library (glibc)**
```
┌─────────────────────────────────────────────────────────────────┐
│                         glibc Overview                         │
└─────────────────────────────────────────────────────────────────┘

Primary Functions:
┌─────────────────────────────────────────────────────────────────┐
│ • System call wrappers                                         │
│ • Standard C library functions                                 │
│ • Memory allocation (malloc, free)                             │
│ • String manipulation functions                                │
│ • Mathematical functions                                       │
│ • Locale and internationalization                              │
│ • Threading support (pthreads)                                │
│ • Dynamic loading support                                      │
└─────────────────────────────────────────────────────────────────┘

Key Components:
┌─────────────────────────────────────────────────────────────────┐
│ libc.so.6     - Main C library                                │
│ libm.so.6     - Math library                                  │
│ libpthread.so - Threading library                             │
│ libdl.so      - Dynamic loading                               │
│ libnss_*.so   - Name Service Switch modules                   │
│ ld-linux.so   - Dynamic linker/loader                         │
└─────────────────────────────────────────────────────────────────┘
```

#### **Library Investigation Commands**
```bash
# Exploring system libraries

# Check glibc version
ldd --version

# Find library dependencies of a program
ldd /bin/ls
ldd /usr/bin/python

# Locate library files
ldconfig -p | grep libc
ldconfig -p | head -20

# Check library information
objdump -p /lib64/libc.so.6 | head -20

# See what libraries are loaded by running process
cat /proc/1/maps | grep -E '\.(so|lib)'

# Check shared library cache
cat /etc/ld.so.cache | strings | head -20

# List all installed libraries
find /lib /lib64 /usr/lib /usr/lib64 -name "*.so*" | head -20

# Check library search paths
echo $LD_LIBRARY_PATH
cat /etc/ld.so.conf
cat /etc/ld.so.conf.d/*
```

---

## 🔄 Process Management Architecture

### **Understanding Process Lifecycle**

#### **Process States and Transitions**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Process State Diagram                       │
└─────────────────────────────────────────────────────────────────┘

                    NEW
                     │
                     ▼
              ┌─────────────┐
              │   READY     │◄──┐
              │ (Runnable)  │   │
              └─────────────┘   │
                     │          │
                     ▼          │
              ┌─────────────┐   │ Timer
              │   RUNNING   │───┤ Interrupt
              │             │   │
              └─────────────┘   │
                │    │    │     │
      I/O Wait  │    │    │     │
                ▼    │    │     │
        ┌─────────────┐   │     │
        │   BLOCKED   │   │     │
        │ (Sleeping)  │───┘     │
        └─────────────┘         │
                                │
                        ┌─────────────┐
                        │ TERMINATED  │
                        │  (Zombie)   │
                        └─────────────┘

Process States in Linux:
• R - Running or Runnable
• S - Interruptible Sleep (waiting for event)
• D - Uninterruptible Sleep (usually I/O)
• T - Stopped (by signal)
• Z - Zombie (terminated but not reaped)
```

#### **Process Creation and Management**
```bash
# Process management commands

# View process hierarchy
ps aux --forest
ps -ef --forest
pstree

# View specific process information
ps -fp 1234  # Replace 1234 with actual PID
cat /proc/1234/status
cat /proc/1234/cmdline

# Monitor processes in real-time
top
htop    # If available
iotop   # I/O monitoring

# Process relationships
ps -eo pid,ppid,cmd | head -20

# View process memory usage
ps aux --sort=-%mem | head -10
cat /proc/meminfo

# Check process file descriptors
ls -la /proc/1234/fd/

# View process environment
cat /proc/1234/environ | tr '\0' '\n'

# Process creation with monitoring
strace -f -e clone,fork,execve bash -c "ls | wc"

# Background process management
sleep 60 &          # Start in background
jobs                # List jobs
fg %1               # Bring to foreground
bg %1               # Send to background
kill %1             # Kill job
```

---

## 🏛️ Monolithic vs Microkernel

### **Kernel Architecture Comparison**

#### **Monolithic Kernel (Linux)**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Monolithic Kernel Design                    │
└─────────────────────────────────────────────────────────────────┘

Architecture:
┌─────────────────────────────────────────────────────────────────┐
│                    User Space                                  │
│ [Applications] [Shell] [Libraries]                             │
├─────────────────────────────────────────────────────────────────┤
│                  System Calls                                  │
├═════════════════════════════════════════════════════════════════┤
│                   Kernel Space                                 │
│ ┌─────────────┬─────────────┬─────────────┬─────────────────┐ │
│ │   Process   │   Memory    │   File      │     Device      │ │
│ │ Management  │ Management  │   System    │    Drivers      │ │
│ └─────────────┴─────────────┴─────────────┴─────────────────┘ │
│ ┌─────────────┬─────────────┬─────────────┬─────────────────┐ │
│ │  Network    │   Security  │   Timer     │      IPC        │ │
│ │   Stack     │   Modules   │  Management │                 │ │
│ └─────────────┴─────────────┴─────────────┴─────────────────┘ │
├─────────────────────────────────────────────────────────────────┤
│                     Hardware                                   │
└─────────────────────────────────────────────────────────────────┘

Characteristics:
✅ Advantages:
• High performance (no message passing overhead)
• Efficient system calls
• Shared kernel data structures
• Good hardware access
• Mature and well-tested

❌ Disadvantages:
• Large kernel size
• Driver bugs can crash system
• Difficult to debug
• Security vulnerabilities affect entire kernel
• Less modular
```

#### **Microkernel Design**
```
┌─────────────────────────────────────────────────────────────────┐
│                     Microkernel Design                         │
└─────────────────────────────────────────────────────────────────┘

Architecture:
┌─────────────────────────────────────────────────────────────────┐
│                    User Space                                  │
│ [Applications]  [File Server]  [Network Server]  [Drivers]     │
├─────────────────────────────────────────────────────────────────┤
│                  Message Passing                               │
├═════════════════════════════════════════════════════════════════┤
│                 Minimal Kernel                                 │
│ ┌─────────────┬─────────────┬─────────────┬─────────────────┐ │
│ │    IPC      │   Process   │   Memory    │    Hardware     │ │
│ │             │ Management  │ Management  │     Access      │ │
│ └─────────────┴─────────────┴─────────────┴─────────────────┘ │
├─────────────────────────────────────────────────────────────────┤
│                     Hardware                                   │
└─────────────────────────────────────────────────────────────────┘

Characteristics:
✅ Advantages:
• Better stability (isolated failures)
• More secure (smaller attack surface)
• Easier debugging
• Modular design
• Better fault tolerance

❌ Disadvantages:
• Performance overhead (message passing)
• Complex implementation
• More context switches
• Larger total system size
```

#### **Linux's Hybrid Approach**
```
Linux Kernel Modules:
┌─────────────────────────────────────────────────────────────────┐
│ Linux combines monolithic and modular approaches:              │
│                                                                 │
│ • Core kernel is monolithic for performance                    │
│ • Loadable modules provide modularity                          │
│ • Modules run in kernel space (not isolated)                   │
│ • Dynamic loading/unloading of drivers                         │
│ • Best of both worlds approach                                 │
└─────────────────────────────────────────────────────────────────┘

Module Commands:
# List loaded modules
lsmod

# Load module
sudo modprobe module_name

# Remove module  
sudo modprobe -r module_name

# Module information
modinfo module_name

# Module dependencies
modprobe --show-depends module_name

# Available modules
find /lib/modules/$(uname -r) -name "*.ko" | head -10
```

---

## 🔧 Device Drivers and Hardware

### **Understanding Hardware Abstraction**

#### **Device Driver Types**
```
┌─────────────────────────────────────────────────────────────────┐
│                      Device Driver Types                       │
└─────────────────────────────────────────────────────────────────┘

Character Devices:
┌─────────────────────────────────────────────────────────────────┐
│ • Stream-oriented devices                                       │
│ • Data transferred byte by byte                                │
│ • Examples: keyboard, mouse, serial ports, terminals           │
│ • Device files: /dev/tty*, /dev/pts/*                         │
│ • Access: Sequential, no random access                         │
└─────────────────────────────────────────────────────────────────┘

Block Devices:
┌─────────────────────────────────────────────────────────────────┐
│ • Block-oriented devices                                        │
│ • Data transferred in fixed-size blocks                        │
│ • Examples: hard drives, SSDs, USB drives                      │
│ • Device files: /dev/sda*, /dev/nvme*                         │
│ • Access: Random access possible                               │
│ • Buffering and caching supported                              │
└─────────────────────────────────────────────────────────────────┘

Network Devices:
┌─────────────────────────────────────────────────────────────────┐
│ • Special category for network interfaces                      │
│ • No device files in /dev                                      │
│ • Examples: eth0, wlan0, lo                                    │
│ • Accessed through socket interface                            │
│ • Managed by network stack                                     │
└─────────────────────────────────────────────────────────────────┘
```

#### **Device File System**
```bash
# Exploring device files

# List device files
ls -la /dev/ | head -20

# Character devices (c)
ls -la /dev/ | grep "^c"

# Block devices (b)  
ls -la /dev/ | grep "^b"

# Major and minor device numbers
ls -la /dev/sda*
# brw-rw---- 1 root disk 8, 0 Nov 15 10:30 /dev/sda
#                         ^  ^
#                    major  minor

# Find devices by major number
ls -la /dev/ | awk '$5 == "8," {print}'

# Check device information
file /dev/sda
file /dev/tty1

# Hardware information commands
lspci          # PCI devices
lsusb          # USB devices  
lscpu          # CPU information
lsblk          # Block devices
lshw           # All hardware (if available)

# Kernel hardware detection
dmesg | grep -i "usb\|pci\|sata"

# Device driver information
cat /proc/devices
cat /proc/modules
```

---

## 💾 Memory Management

### **Understanding Virtual Memory**

#### **Memory Management Concepts**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Virtual Memory Layout                       │
└─────────────────────────────────────────────────────────────────┘

Process Virtual Memory (64-bit):
┌─────────────────────────────────────────────────────────────────┐
│ 0x7FFFFFFFFFFF ┌─────────────────────────────────────────────┐ │
│                │           Kernel Space                      │ │
│                │        (not accessible)                     │ │
│ 0x800000000000 ├─────────────────────────────────────────────┤ │
│                │              Gap                            │ │
│                ├─────────────────────────────────────────────┤ │
│                │           Stack (grows down)                │ │
│                │              ↓                              │ │
│                ├─────────────────────────────────────────────┤ │
│                │           Memory Mapped Files              │ │
│                ├─────────────────────────────────────────────┤ │
│                │              ↑                              │ │
│                │           Heap (grows up)                   │ │
│                ├─────────────────────────────────────────────┤ │
│                │           Uninitialized Data (BSS)          │ │
│                ├─────────────────────────────────────────────┤ │
│                │           Initialized Data                  │ │
│                ├─────────────────────────────────────────────┤ │
│                │           Program Text (Code)               │ │
│ 0x400000       └─────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

#### **Memory Information Commands**
```bash
# Memory investigation commands

# System memory information
free -h
cat /proc/meminfo

# Per-process memory usage
ps aux --sort=-%mem | head -10
top -o %MEM

# Virtual memory statistics
vmstat 1 5

# Memory mapping of a process
cat /proc/self/maps
cat /proc/1/maps | head -10

# Memory allocation information
cat /proc/meminfo | grep -E "(MemTotal|MemFree|MemAvailable|Buffers|Cached)"

# Swap information
cat /proc/swaps
swapon --show

# Memory usage by process
pmap 1234  # Replace with actual PID

# System memory pressure
cat /proc/pressure/memory

# OOM (Out of Memory) killer information
dmesg | grep -i "killed process"

# Memory fragmentation
cat /proc/buddyinfo

# Check for memory leaks
valgrind --leak-check=full command_name
```

---

## 🎯 Interview Questions

### **Architecture and Components Interview Questions**

#### **Question 1: Kernel Space vs User Space**
```
Q: Explain the difference between kernel space and user space. Why is this 
   separation important?

Expected Answer:
- Kernel space: Privileged mode, direct hardware access, no memory protection
- User space: Restricted mode, system calls for kernel services, memory protected
- Separation provides stability (crashes contained) and security
- System calls provide controlled interface between spaces
- Examples of each space's contents
```

#### **Question 2: systemd vs SysV Init**
```
Q: What are the main advantages of systemd over traditional SysV init?

Expected Answer:
- Parallel startup vs sequential
- Dependency management 
- Socket activation
- Process supervision and restart
- Integrated logging with journald
- Modern unit files vs shell scripts
- Better resource management with cgroups
```

#### **Question 3: Process States**
```
Q: What are the different process states in Linux? Describe when a process 
   would be in each state.

Expected Answer:
- Running (R): Currently executing or ready to run
- Sleeping (S): Waiting for event (interruptible)
- Uninterruptible Sleep (D): Usually waiting for I/O
- Stopped (T): Suspended by signal
- Zombie (Z): Terminated but not reaped by parent
- Give practical examples of each
```

#### **Question 4: Memory Management**
```
Q: How does Linux handle virtual memory? What are the benefits?

Expected Answer:
- Each process has own virtual address space
- Memory mapping unit (MMU) translates virtual to physical
- Benefits: Process isolation, memory protection, efficient use of RAM
- Swapping allows processes larger than physical memory
- Copy-on-write for efficient fork()
```

---

## 🎯 Summary and Next Steps

### **Day 5 Accomplishments**

✅ **Architecture and Components Mastery Achieved:**
- Complete Linux system architecture understanding
- Kernel vs user space boundary comprehension
- Kernel subsystems and components knowledge
- Init system evolution and systemd mastery
- System libraries and API layer understanding
- Process management architecture
- Monolithic vs microkernel comparison
- Device driver system understanding
- Memory management concepts

### **Key Takeaways:**
```
Essential Architecture Concepts:
┌─────────────────────────────────────────────────────────────────┐
│ • Linux uses layered architecture for modularity               │
│ • Kernel/user space separation provides stability & security   │
│ • systemd brings modern process management to Linux            │
│ • Virtual memory enables efficient resource utilization        │
│ • Everything in Linux is abstracted as files or processes      │
│ • Understanding architecture helps troubleshooting             │
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