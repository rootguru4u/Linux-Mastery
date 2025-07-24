# 🌐 **Linux Mastery Training Syllabus**

---
**📚 Course:** rootguru Linux Classes  
**🌐 Website:** [www.rootguru.info](http://www.rootguru.info)  
**📖 Document:** Linux Administration Professional Program  
**🎯 Target:** Absolute beginners to skilled Linux administrators  
**⏱️ Duration:** 18 Modules | Comprehensive Program  
**👨‍🏫 Created by:** rootguru Team  

---

## 📋 **Table of Contents**

| Module | Topic |
|--------|--------|
| **1** | Introduction to Linux, Filesystem, Linux file system heirarchy |
| **2** | Linux Installation & Initial Setup |
| **3** | File Management, Viewing & Searching |
| **4** | Text Processing, Redirection & Pipes |
| **5** | Users, Groups, and Permissions |
| **6** | Package, Process & Job Management |
| **7** | Archive, Compression & Backup |
| **8** | Default Linux System Configuration & Customization |
| **9** | Disk, LVM, and Filesystem Management |
| **10** | Boot Process, Recovery & Kernel Issues |
| **11** | Network, Remote Access & Services |
| **12** | File Sharing Services |
| **13** | Web & Application Services |
| **14** | RAID, LUN, and Advanced Storage |
| **15** | OS Hardening & Patching |
| **16** | Monitoring, Logs & Troubleshooting |
| **17** | Linux Clustering Basics |
| **18** | Capstone Projects |

---

## **Module 1: Introduction to Linux**

### Topics Covered:
- Operating System fundamentals and Linux introduction
- Linux vs Windows: Key differences and use cases
- Linux distributions (RHEL, CentOS, Ubuntu, SUSE)
- GNU Project and open source licensing (GPL, MIT, Apache)
- Linux architecture: Kernel vs User Space
- Linux system components and process management
- Accessing Linux (VMware, Cloud, Dual Boot, Live Boot)
- CLI vs GUI understanding
- Basic terminal navigation and help systems
- Pseudo filesystems (/proc, /sys) exploration
- Terminal multiplexers (tmux, screen) basics
- Linux philosophy and community culture

---

## **Module 2: Linux Installation & Initial Setup**

### Topics Covered:
- VMware/VirtualBox setup for Linux environments
- CentOS 7/8 installation (auto & manual partitioning)
- Enterprise installation planning and media management
- Boot sequence and firmware considerations (BIOS/UEFI)
- Filesystem selection (ext4, xfs, btrfs) and optimization
- LVM planning and architecture during installation
- Network configuration and hostname setup
- Installation automation concepts (Kickstart, PXE)
- Post-installation system configuration
- Documentation and compliance standards

---

## **Module 3: File Management, Viewing & Searching**

### Topics Covered:
- File and directory operations: ls, cd, pwd, mkdir, touch, rm, cp, mv, tree
- File viewing tools: cat, tac, less, more, head, tail
- File search tools: find, locate, whereis, which, basename, dirname
- Wildcards and globbing patterns
- File linking: hard links and symbolic links
- File compression and archiving basics
- Directory navigation optimization
- File system hierarchy and organization
- Advanced file operations and batch processing

---

## **Module 4: Text Processing, Redirection & Pipes**

### Topics Covered:
- Text processing commands: cut, sort, uniq, wc, tee, xargs, tr, paste
- Input/Output redirection: >, >>, <, |, 2>, 2>&1
- Command chaining and pipes
- Advanced text tools: grep, awk, sed
- Command substitution and variables
- Here documents and strings
- Regular expressions fundamentals
- Process substitution and named pipes
- Text manipulation for automation

---

## **Module 5: Users, Groups, and Permissions**

### Topics Covered:
- User management: useradd, passwd, usermod, userdel, chage
- Group management: groupadd, groupmod, groups, id
- File permissions: chmod, chown, umask, stat
- Advanced permissions: SUID, SGID, Sticky bit
- Access Control Lists (ACLs): getfacl, setfacl
- Password policies and account security
- sudo configuration and privilege escalation
- User environment management
- Account lockout and password recovery

---

## **Module 6: Package, Process & Job Management**

### Topics Covered:
- Package management: yum, rpm, dnf, dependency resolution
- Repository configuration and management
- Process monitoring: ps, top, htop, pstree
- Process control: kill, killall, nice, renice, nohup
- Background jobs: &, fg, bg, jobs, disown
- Service management: systemctl (start, stop, enable, disable, status)
- Systemd units and service creation
- Job scheduling: cron, crontab, systemd timers
- System performance monitoring and resource limits

---

## **Module 7: Archive, Compression & Backup**

### Topics Covered:
- Archive tools: tar, zip, unzip, gzip, gunzip, xz, bzip2
- Backup strategies: full, incremental, differential backups
- Remote backup: rsync, scp, cloud integration
- Backup automation and scheduling
- Data compression algorithms and optimization
- Backup verification and integrity checking
- Disaster recovery planning and procedures
- Backup rotation and retention policies

---

## **Module 8: Default Linux System Configuration & Customization**

### Topics Covered:
- Systemd targets vs runlevels: systemctl get-default, set-default
- Shell profile hierarchy: /etc/profile, ~/.bashrc, ~/.bash_profile
- Command history variables: HISTSIZE, HISTTIMEFORMAT, HISTIGNORE
- PS1 prompt customization with color codes
- Creating and managing aliases
- Hostname and locale configuration: hostnamectl, localectl
- Auto logout using TMOUT variable
- Login banners: /etc/motd, /etc/issue, /etc/issue.net
- User defaults: umask, /etc/skel directory
- Environment variables and system-wide configuration
- PAM configuration: /etc/security/limits.conf, /etc/login.defs

---

## **Module 9: Disk, LVM, and Filesystem Management**

### Topics Covered:
- Disk partitioning: fdisk, parted, lsblk, blkid
- Filesystem creation: mkfs.ext4, mkfs.xfs, mkfs.btrfs
- Mount operations: mount, umount, /etc/fstab
- Logical Volume Management: pvcreate, vgcreate, lvcreate, lvextend
- Filesystem expansion: resize2fs, xfs_growfs
- LVM snapshots and thin provisioning
- Filesystem checking and repair: fsck, xfs_repair
- Disk usage monitoring: df, du, quota management
- Storage performance optimization and tuning

---

## **Module 10: Boot Process, Recovery & Kernel Issues**

### Topics Covered:
- Linux boot process: BIOS/UEFI → GRUB → Kernel → systemd
- GRUB configuration and management: grub2-mkconfig, grub2-install
- Boot parameters and kernel options
- initramfs and dracut management
- Single-user mode and recovery procedures
- Emergency and rescue mode operations
- Kernel compilation and module management
- Boot troubleshooting and repair procedures
- System recovery and disaster scenarios

---

## **Module 11: Network, Remote Access & Services**

### Topics Covered:
- Network configuration: nmcli, ip, ifconfig, ethtool
- Static and DHCP configuration
- DNS configuration: /etc/resolv.conf, /etc/hosts
- SSH configuration and key-based authentication
- FTP services: vsftpd setup and configuration
- SFTP secure transfer and chroot jails
- DHCP server setup and management
- Network troubleshooting: ping, traceroute, netstat, ss
- Remote access security and monitoring

---

## **Module 12: File Sharing Services**

### Topics Covered:
- NFS server and client configuration
- NFS exports and permanent mounting
- SAMBA/CIFS setup for Linux-Windows integration
- SAMBA authentication and user management
- Network storage architecture: NAS vs SAN concepts
- File sharing security and access control
- Cross-platform file sharing optimization
- Storage networking and performance tuning

---

## **Module 13: Web & Application Services**

### Topics Covered:
- Apache HTTP server: installation and configuration
- Virtual hosts and document root management
- NGINX setup and reverse proxy configuration
- SSL/TLS configuration and certificate management
- Firewall configuration: firewalld and iptables
- Web server security and hardening
- Load balancing and high availability
- Application deployment and management

---

## **Module 14: RAID, LUN, and Advanced Storage**

### Topics Covered:
- RAID concepts and levels: RAID 0, 1, 5, 10
- Software RAID with mdadm: creation and management
- LUN concepts and storage networking
- iSCSI target and initiator configuration
- Multipath storage and redundancy
- Storage area networks (SAN) and network attached storage (NAS)
- Advanced storage troubleshooting
- Storage performance optimization

---

## **Module 15: OS Hardening & Patching**

### Topics Covered:
- System security assessment and hardening
- Service management and attack surface reduction
- SSH security: port changes, root login restrictions, timeouts
- sudo configuration and access control
- Package management security and minimal installations
- Patch management: yum update, dnf upgrade procedures
- AWS AMI patching automation and scheduling
- Security compliance and audit requirements
- Vulnerability scanning and remediation

---

## **Module 16: Monitoring, Logs & Troubleshooting**

### Topics Covered:
- System logs: /var/log directory structure and analysis
- journalctl for systemd log management
- Log rotation: logrotate configuration and management
- System monitoring: top, vmstat, iostat, netstat, ss
- Performance monitoring and trending
- Custom monitoring scripts and automation
- Alert systems and notification setup
- Troubleshooting methodologies and best practices

---

## **Module 17: Linux Clustering Basics**

### Topics Covered:
- Clustering concepts: High Availability and Load Balancing
- Pacemaker and Corosync cluster suite
- Keepalived for load balancing and failover
- Cluster resource management and constraints
- Split-brain prevention and quorum
- Service failover and recovery procedures
- Cluster monitoring and management
- High availability design patterns

---

## **Module 18: Capstone Projects**

### Topics Covered:
- SAMBA shared folder project (Linux ↔ Windows integration)
- Web cluster with Keepalived and Apache high availability
- FTP/SFTP secure transfer setup and automation
- System patching with rollback planning (AWS + automation)
- LVM backup and recovery system implementation
- SSH hardening with custom banners and monitoring
- Log analyzer script development and deployment
- Enterprise infrastructure integration projects

---

## 📞 **About rootguru**

**🐧 Professional Linux Training** • [www.rootguru.info](http://www.rootguru.info)

*Transform absolute beginners into skilled Linux administrators with 3–4 years equivalent experience*

### 🎯 **Why Choose rootguru?**
- ✅ **Industry-Focused**: Real-world scenarios and enterprise skills
- ✅ **Expert Instructors**: 8+ years Linux administration experience  
- ✅ **Career Support**: Job placement assistance and interview preparation
- ✅ **Flexible Learning**: Online, weekend, and corporate training available
- ✅ **Comprehensive Coverage**: 18 modules covering all essential Linux skills
- ✅ **Hands-on Approach**: Practical training with real-world projects

### 📞 **Get Started Today**
- 🌐 **Website**: [www.rootguru.info](http://www.rootguru.info)
- 📧 **Email**: info@rootguru.info
- 📱 **WhatsApp**: +91-8459777100 (Training inquiries)
- 💼 **LinkedIn**: Connect for career opportunities and updates

### 🚀 **Course Highlights**
- **18 Comprehensive Modules** covering beginner to advanced topics
- **Enterprise-level Skills** for professional Linux administration
- **Capstone Projects** for hands-on experience and portfolio building
- **Job Placement Support** with interview preparation and career guidance
- **Industry Recognition** for quality Linux training and certification

**© rootguru Linux Classes** | *Empowering Linux Administration Through Practical Learning*

---

**Transform Your Career - From Absolute Beginner to Skilled Linux Professional!** 
