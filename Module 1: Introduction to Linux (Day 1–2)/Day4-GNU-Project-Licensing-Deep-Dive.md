# Day 4: GNU Project & Licensing Deep Dive

---
**📚 Course:** rootguru Linux Classes  
**🌐 Website:** [www.rootguru.info](http://www.rootguru.info)  
**📖 Document:** Linux Fundamentals - Day 4 GNU & Licensing Guide  
**🎯 Level:** Absolute Beginner  
**⏱️ Duration:** 4-5 hours  
**💻 Platform:** CentOS 7 / RHEL 7  
**👨‍🏫 Created by:** rootguru Team  

---

## 📖 Table of Contents

1. [The GNU Project Foundation](#the-gnu-project-foundation)
2. [Understanding Free Software Philosophy](#understanding-free-software-philosophy)
3. [GPL and Open Source Licensing](#gpl-and-open-source-licensing)
4. [License Types and Comparisons](#license-types-and-comparisons)
5. [Commercial Implications and Business Models](#commercial-implications-and-business-models)
6. [Linux Distribution Licensing](#linux-distribution-licensing)
7. [Practical License Investigation](#practical-license-investigation)
8. [Open Source vs Proprietary Software](#open-source-vs-proprietary-software)
9. [Community and Development Model](#community-and-development-model)
10. [Interview Questions](#interview-questions)

---

## 🏛️ The GNU Project Foundation

### **Understanding the Origins of Free Software**

#### **What is GNU?**
```
┌─────────────────────────────────────────────────────────────────┐
│                    GNU Project Overview                        │
└─────────────────────────────────────────────────────────────────┘

GNU = "GNU's Not Unix" (Recursive Acronym)
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  Started: 1983 by Richard Stallman                             │
│  Goal: Create a completely free Unix-like operating system     │
│  Philosophy: Software should be free for everyone              │
│                                                                 │
│  Key Components GNU Developed:                                 │
│  ├── GCC (GNU Compiler Collection)                            │
│  ├── Bash (Bourne Again Shell)                                │
│  ├── Emacs (Text Editor)                                      │
│  ├── Coreutils (ls, cp, mv, etc.)                            │
│  ├── Make (Build automation tool)                             │
│  └── Thousands of other tools                                 │
│                                                                 │
│  Missing Piece: Kernel                                         │
│  └── Linux Kernel (1991) completed the puzzle                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### **Timeline of GNU Development**
```
GNU Project Timeline:
┌─────────────────────────────────────────────────────────────────┐
│ 1983 │ Richard Stallman announces GNU Project                  │
│ 1984 │ Stallman leaves MIT to work on GNU full-time           │
│ 1985 │ Free Software Foundation (FSF) established             │
│ 1987 │ GCC (GNU C Compiler) first released                    │
│ 1989 │ GPL version 1 published                                │
│ 1990 │ Emacs, GDB, and other tools mature                     │
│ 1991 │ Linux kernel fills the missing piece                   │
│ 1992 │ GNU/Linux complete operating system available          │
│ 1991 │ GPL version 2 published                                │
│ 2007 │ GPL version 3 published                                │
│ 2024 │ GNU powers billions of devices worldwide               │
└─────────────────────────────────────────────────────────────────┘
```

#### **Richard Stallman's Vision**
```
The Four Essential Freedoms (1983):
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  Freedom 0: Run the program for any purpose                    │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Use software for business, personal, educational     │   │
│  │ • No restrictions on who can use it                    │   │
│  │ • No restrictions on where it can be used              │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Freedom 1: Study and modify the source code                   │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Access to complete source code                       │   │
│  │ • Right to understand how software works               │   │
│  │ • Right to fix bugs and add features                   │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Freedom 2: Distribute copies to help others                   │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Share original software with anyone                  │   │
│  │ • Can charge for distribution service                  │   │
│  │ • Help build community                                 │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Freedom 3: Distribute modified versions                       │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Share your improvements with community               │   │
│  │ • Must provide source code of modifications            │   │
│  │ • Everyone benefits from improvements                  │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔓 Understanding Free Software Philosophy

### **Free Software vs Open Source Movement**

#### **Free Software Foundation (FSF) Principles**
```
┌─────────────────────────────────────────────────────────────────┐
│               Free Software vs Open Source                     │
└─────────────────────────────────────────────────────────────────┘

Free Software Movement (1983):
┌─────────────────────────────────────────────────────────────────┐
│ Focus: ETHICAL foundation of software freedom                  │
│ Leader: Richard Stallman, Free Software Foundation             │
│ Philosophy:                                                     │
│ • Software freedom is a social justice issue                   │
│ • Proprietary software is inherently unethical                 │
│ • Users have fundamental right to control their computing      │
│ • "Free as in Freedom, not just Free Beer"                    │
│                                                                 │
│ Terminology: "Free Software"                                   │
│ License: GPL (strong copyleft)                                 │
└─────────────────────────────────────────────────────────────────┘

Open Source Movement (1998):
┌─────────────────────────────────────────────────────────────────┐
│ Focus: PRACTICAL benefits of collaborative development         │
│ Leader: Eric Raymond, Open Source Initiative                   │
│ Philosophy:                                                     │
│ • Better software through peer review                          │
│ • Business-friendly approach                                   │
│ • Focus on development methodology                             │
│ • "Given enough eyeballs, all bugs are shallow"               │
│                                                                 │
│ Terminology: "Open Source Software"                            │
│ License: Various (MIT, Apache, BSD, GPL)                       │
└─────────────────────────────────────────────────────────────────┘
```

#### **Why GNU/Linux and Not Just Linux?**
```
The Naming Controversy Explained:
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  GNU advocates prefer "GNU/Linux" because:                     │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • GNU tools make up majority of the system             │   │
│  │ • Linux is just the kernel (important but small part)  │   │
│  │ • GNU project started 8 years before Linux             │   │
│  │ • Gives credit to GNU's philosophical foundation       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Most people just say "Linux" because:                         │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Shorter and easier to say                            │   │
│  │ • Linux kernel is the unique differentiator            │   │
│  │ • Industry standard terminology                        │   │
│  │ • Less confusing for newcomers                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Technical Reality:                                             │
│  Linux Kernel + GNU Tools + Other Software = Complete OS       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📜 GPL and Open Source Licensing

### **Understanding the GNU General Public License**

#### **GPL Version History and Evolution**
```
┌─────────────────────────────────────────────────────────────────┐
│                    GPL Version Comparison                      │
└─────────────────────────────────────────────────────────────────┘

GPL v1 (1989):
┌─────────────────────────────────────────────────────────────────┐
│ • First formal version of GPL                                  │
│ • Established basic copyleft principle                         │
│ • Required source code sharing                                 │
│ • Short and simple (about 2 pages)                            │
└─────────────────────────────────────────────────────────────────┘

GPL v2 (1991):
┌─────────────────────────────────────────────────────────────────┐
│ • Most widely used version (Linux kernel uses this)            │
│ • Added patent protection clauses                              │
│ • Clarified distribution requirements                          │
│ • Added "Liberty or Death" clause (Section 7)                  │
│ • Better international compatibility                           │
│ • About 4 pages long                                           │
└─────────────────────────────────────────────────────────────────┘

GPL v3 (2007):
┌─────────────────────────────────────────────────────────────────┐
│ • Addresses modern issues (DRM, patents, hardware)             │
│ • Anti-tivoization provisions                                  │
│ • Enhanced patent protection                                   │
│ • Better international law compatibility                       │
│ • Network copyleft (AGPL connection)                          │
│ • About 7 pages long                                           │
│ • Controversial - Linus Torvalds rejected for Linux kernel     │
└─────────────────────────────────────────────────────────────────┘
```

#### **How GPL Works: Copyleft Explained**
```
Copyleft Mechanism:
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  Traditional Copyright: "All Rights Reserved"                  │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Author controls copying, modification, distribution     │   │
│  │ Others need permission for any use                      │   │
│  │ Creates proprietary software                           │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Copyleft: "All Rights Reversed"                              │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Author grants freedoms but with conditions             │   │
│  │ Must preserve freedoms in derivative works             │   │
│  │ Creates "viral" effect - spreads freedom               │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  GPL Viral Effect:                                             │
│  Original GPL Code → Modified Code → Must Also Be GPL          │
│                                                                 │
│  Exception: Linking and Fair Use                               │
│  • Dynamic linking may not trigger copyleft                   │
│  • System libraries have special exception                    │
│  • Mere aggregation doesn't trigger copyleft                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## ⚖️ License Types and Comparisons

### **Understanding Different Open Source Licenses**

#### **Comprehensive License Comparison**
```
┌─────────────────────────────────────────────────────────────────┐
│                    License Comparison Matrix                   │
└─────────────────────────────────────────────────────────────────┘

Copyleft Licenses (Viral):
┌──────────────┬─────────────────┬─────────────────┬─────────────────┐
│   License    │   Viral Effect  │  Patent Terms   │   Complexity    │
├──────────────┼─────────────────┼─────────────────┼─────────────────┤
│ GPL v2       │ Strong          │ Basic           │ Medium          │
│ GPL v3       │ Strong          │ Comprehensive   │ High            │
│ LGPL         │ Weak (libraries)│ Same as GPL     │ High            │
│ AGPL         │ Network Strong  │ Same as GPL v3  │ Very High       │
│ MPL 2.0      │ File-level      │ Good            │ Medium          │
└──────────────┴─────────────────┴─────────────────┴─────────────────┘

Permissive Licenses (Non-viral):
┌──────────────┬─────────────────┬─────────────────┬─────────────────┐
│   License    │  Business Use   │  Patent Terms   │   Attribution   │
├──────────────┼─────────────────┼─────────────────┼─────────────────┤
│ MIT          │ Unrestricted    │ None            │ Copyright only  │
│ BSD 2-Clause │ Unrestricted    │ None            │ Copyright only  │
│ BSD 3-Clause │ Unrestricted    │ None            │ Copyright + No  │
│              │                 │                 │ endorsement     │
│ Apache 2.0   │ Unrestricted    │ Comprehensive   │ Copyright +     │
│              │                 │                 │ Attribution     │
│ ISC          │ Unrestricted    │ None            │ Copyright only  │
└──────────────┴─────────────────┴─────────────────┴─────────────────┘
```

#### **Practical License Examples**
```
Real-World License Usage:
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  GPL Projects:                                                  │
│  • Linux Kernel (GPL v2)                                       │
│  • MySQL (GPL v2, with commercial option)                      │
│  • WordPress (GPL v2+)                                         │
│  • GIMP (GPL v3+)                                              │
│  • VLC Media Player (GPL v2+)                                  │
│                                                                 │
│  MIT License Projects:                                          │
│  • Node.js runtime                                             │
│  • React.js library                                            │
│  • jQuery library                                              │
│  • Ruby on Rails framework                                     │
│  • .NET Core                                                   │
│                                                                 │
│  Apache License Projects:                                       │
│  • Apache HTTP Server                                          │
│  • Kubernetes                                                  │
│  • Android Open Source Project                                 │
│  • Hadoop ecosystem                                            │
│  • Swift programming language                                  │
│                                                                 │
│  BSD License Projects:                                          │
│  • FreeBSD operating system                                    │
│  • PostgreSQL database                                         │
│  • Nginx web server                                            │
│  • OpenSSH                                                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 💼 Commercial Implications and Business Models

### **How Companies Make Money with Open Source**

#### **Business Models Around Open Source**
```
┌─────────────────────────────────────────────────────────────────┐
│                 Open Source Business Models                    │
└─────────────────────────────────────────────────────────────────┘

1. Dual Licensing:
┌─────────────────────────────────────────────────────────────────┐
│ Example: MySQL                                                  │
│ • Community Edition: GPL (free, copyleft)                      │
│ • Commercial License: Pay to avoid GPL requirements            │
│ • Customers: Want to embed MySQL in proprietary software       │
│ • Revenue: License fees from commercial users                  │
└─────────────────────────────────────────────────────────────────┘

2. Support and Services:
┌─────────────────────────────────────────────────────────────────┐
│ Example: Red Hat                                                │
│ • Software: Free (CentOS, Fedora)                             │
│ • Revenue: Support contracts, training, consulting             │
│ • Value: Enterprise reliability, guaranteed updates            │
│ • Customers: Pay for peace of mind and professional support    │
└─────────────────────────────────────────────────────────────────┘

3. Open Core:
┌─────────────────────────────────────────────────────────────────┐
│ Example: GitLab                                                 │
│ • Core: Open source version (Community Edition)                │
│ • Premium: Additional proprietary features (Enterprise)        │
│ • Revenue: Subscription fees for enterprise features           │
│ • Strategy: Hook users with free version, upsell premium       │
└─────────────────────────────────────────────────────────────────┘

4. Software-as-a-Service (SaaS):
┌─────────────────────────────────────────────────────────────────┐
│ Example: GitHub                                                 │
│ • Software: Git is open source                                 │
│ • Service: Hosted Git repositories with additional features    │
│ • Revenue: Monthly subscriptions for hosted service            │
│ • Value: Convenience, collaboration tools, integration         │
└─────────────────────────────────────────────────────────────────┘
```

#### **Corporate Open Source Strategies**
```
Why Companies Contribute to Open Source:
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  Strategic Benefits:                                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Reduce development costs (shared development)         │   │
│  │ • Attract talented developers                           │   │
│  │ • Set industry standards                                │   │
│  │ • Build ecosystem around their platform                │   │
│  │ • Improve software quality (many eyes principle)       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Examples:                                                      │
│  • Google: Releases Android, Kubernetes, TensorFlow            │
│  • Microsoft: .NET Core, PowerShell, VS Code                   │
│  • Facebook: React, GraphQL, PyTorch                           │
│  • Amazon: Many AWS tools and libraries                        │
│  • IBM: Red Hat acquisition, OpenShift, Cloud tools            │
│                                                                 │
│  Risk Management:                                               │
│  • Avoid vendor lock-in                                        │
│  • Ensure software survival beyond original company            │
│  • Benefit from community security reviews                     │
│  • Reduce maintenance burden through community               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🐧 Linux Distribution Licensing

### **How Distributions Handle Licensing**

#### **Distribution Licensing Approaches**
```
┌─────────────────────────────────────────────────────────────────┐
│              Distribution License Strategies                   │
└─────────────────────────────────────────────────────────────────┘

Debian Approach:
┌─────────────────────────────────────────────────────────────────┐
│ • Debian Free Software Guidelines (DFSG)                       │
│ • Strict separation: main, contrib, non-free                   │
│ • Main repository: Only DFSG-compliant licenses                │
│ • Non-free: Available but clearly separated                    │
│ • Philosophy: Ideological purity                               │
└─────────────────────────────────────────────────────────────────┘

Red Hat/CentOS Approach:
┌─────────────────────────────────────────────────────────────────┐
│ • Pragmatic approach to enterprise needs                       │
│ • Includes some proprietary firmware                           │
│ • Clear license documentation                                  │
│ • RHEL: Commercial support model                               │
│ • CentOS: Community rebuild (until stream)                     │
└─────────────────────────────────────────────────────────────────┘

Ubuntu Approach:
┌─────────────────────────────────────────────────────────────────┐
│ • Four repositories: main, restricted, universe, multiverse    │
│ • Main: Canonical-supported open source                        │
│ • Restricted: Proprietary drivers for hardware support         │
│ • Universe: Community-maintained open source                   │
│ • Multiverse: Software not meeting main criteria               │
└─────────────────────────────────────────────────────────────────┘
```

#### **Checking Licenses in Your System**
```bash
# Commands to investigate licensing in CentOS/RHEL:

# Check package license information
rpm -qi package_name | grep License

# Example: Check bash license
rpm -qi bash | grep License
# License: GPLv3+

# List all packages and their licenses
rpm -qa --qf '%{NAME}-%{VERSION}-%{RELEASE}: %{LICENSE}\n' | head -20

# Check specific license directory
ls /usr/share/licenses/

# View specific license text
cat /usr/share/licenses/bash*/COPYING

# Find GPL-licensed packages
rpm -qa --qf '%{NAME}: %{LICENSE}\n' | grep -i gpl

# Find MIT-licensed packages  
rpm -qa --qf '%{NAME}: %{LICENSE}\n' | grep -i mit

# Check what license a file belongs to
rpm -qf /bin/ls
rpm -qi coreutils | grep License
```

---

## 🔍 Practical License Investigation

### **Hands-on License Analysis**

#### **Lab Exercise: System License Audit**
```bash
# Exercise 1: Basic License Investigation
# Create a script to audit system licenses

#!/bin/bash
# license_audit.sh - System License Audit Script

echo "=== System License Audit ==="
echo "Date: $(date)"
echo "Hostname: $(hostname)"
echo ""

echo "=== Most Common Licenses ==="
rpm -qa --qf '%{LICENSE}\n' | sort | uniq -c | sort -rn | head -10

echo ""
echo "=== GPL Licensed Packages ==="
rpm -qa --qf '%{NAME}: %{LICENSE}\n' | grep -i gpl | head -10

echo ""
echo "=== MIT Licensed Packages ==="
rpm -qa --qf '%{NAME}: %{LICENSE}\n' | grep -i mit | head -5

echo ""
echo "=== Apache Licensed Packages ==="
rpm -qa --qf '%{NAME}: %{LICENSE}\n' | grep -i apache | head -5

echo ""
echo "=== Proprietary/Commercial Packages ==="
rpm -qa --qf '%{NAME}: %{LICENSE}\n' | grep -vE '(GPL|MIT|BSD|Apache|Public Domain)' | head -5
```

#### **Source Code License Investigation**
```bash
# Exercise 2: Finding License Information in Source Code

# Common license file names to look for:
find /usr/src -name "LICENSE*" -type f 2>/dev/null | head -5
find /usr/src -name "COPYING*" -type f 2>/dev/null | head -5
find /usr/src -name "COPYRIGHT*" -type f 2>/dev/null | head -5

# Check kernel source license
cat /usr/src/kernels/*/COPYING 2>/dev/null | head -20

# Look for license headers in source files
head -20 /usr/include/stdio.h | grep -i license

# Check documentation directories
ls /usr/share/doc/ | head -10
ls /usr/share/doc/bash*/
```

#### **Web Service License Checking**
```bash
# Exercise 3: Checking licenses of installed web components

# If Apache is installed
rpm -qi httpd | grep License 2>/dev/null

# If PHP is installed  
rpm -qi php | grep License 2>/dev/null

# If MySQL/MariaDB is installed
rpm -qi mariadb-server | grep License 2>/dev/null

# Check python packages (if pip is available)
pip list --format=columns 2>/dev/null | head -10

# Create summary report
echo "System: $(cat /etc/os-release | grep PRETTY_NAME)"
echo "Kernel: $(uname -r)"
echo "Total packages: $(rpm -qa | wc -l)"
echo "GPL packages: $(rpm -qa --qf '%{LICENSE}\n' | grep -i gpl | wc -l)"
echo "MIT packages: $(rpm -qa --qf '%{LICENSE}\n' | grep -i mit | wc -l)"
```

---

## 🏢 Open Source vs Proprietary Software

### **Understanding the Fundamental Differences**

#### **Development Model Comparison**
```
┌─────────────────────────────────────────────────────────────────┐
│            Open Source vs Proprietary Development              │
└─────────────────────────────────────────────────────────────────┘

Open Source Development:
┌─────────────────────────────────────────────────────────────────┐
│ Characteristics:                                                │
│ • Public source code repository                                │
│ • Community-driven development                                 │
│ • Transparent decision-making                                  │
│ • Distributed development team                                 │
│ • Merit-based leadership                                       │
│                                                                 │
│ Quality Assurance:                                              │
│ • "Many eyes make all bugs shallow"                            │
│ • Public security review                                       │
│ • Rapid patch deployment                                       │
│ • Community testing                                            │
│                                                                 │
│ Examples: Linux, Apache, Firefox, PostgreSQL                   │
└─────────────────────────────────────────────────────────────────┘

Proprietary Development:
┌─────────────────────────────────────────────────────────────────┐
│ Characteristics:                                                │
│ • Closed source code                                           │
│ • Company-controlled development                               │
│ • Business-driven decisions                                    │
│ • Centralized development team                                 │
│ • Management hierarchy                                         │
│                                                                 │
│ Quality Assurance:                                              │
│ • Professional QA teams                                        │
│ • Controlled release cycles                                    │
│ • Limited security review                                      │
│ • Customer-driven testing                                      │
│                                                                 │
│ Examples: Windows, macOS, Oracle Database, Adobe Creative Suite │
└─────────────────────────────────────────────────────────────────┘
```

#### **Security Implications**
```
Security Model Comparison:
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  Open Source Security:                                          │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Pros:                                                   │   │
│  │ • Transparent security review                           │   │
│  │ • Rapid vulnerability patching                          │   │
│  │ • No security through obscurity                        │   │
│  │ • Community vigilance                                   │   │
│  │ • Independent security audits possible                 │   │
│  │                                                         │   │
│  │ Cons:                                                   │   │
│  │ • Vulnerabilities visible to attackers                 │   │
│  │ • Uncoordinated disclosure possible                    │   │
│  │ • Quality varies by project                            │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Proprietary Security:                                          │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Pros:                                                   │   │
│  │ • Controlled disclosure process                         │   │
│  │ • Professional security teams                          │   │
│  │ • Coordinated patch releases                           │   │
│  │ • Liability and support guarantees                     │   │
│  │                                                         │   │
│  │ Cons:                                                   │   │
│  │ • Limited external review                              │   │
│  │ • Slower patch cycles                                  │   │
│  │ • Security through obscurity                          │   │
│  │ • Vendor dependency                                    │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🌍 Community and Development Model

### **Understanding Open Source Communities**

#### **Community Structure and Governance**
```
┌─────────────────────────────────────────────────────────────────┐
│                 Linux Kernel Community Structure               │
└─────────────────────────────────────────────────────────────────┘

Hierarchy:
                    Linus Torvalds
                   (Benevolent Dictator)
                          │
            ┌─────────────┼─────────────┐
            │             │             │
    Subsystem Maintainers │    Andrew Morton
    (Network, Filesystem, │    (Memory Management)
     Security, etc.)      │
            │             │             │
    ┌───────┴─────────────┼─────────────┴───────┐
    │                     │                     │
Individual Contributors   │        Companies
(Patches, bug reports)    │        (Red Hat, Intel,
                          │         IBM, Google)
                          │
                   Git Repository
                (Source Code Control)

Development Process:
1. Developer writes patch
2. Submit to mailing list
3. Review and discussion
4. Maintainer approval
5. Integration into main tree
6. Testing and release
```

#### **Contribution Guidelines and Etiquette**
```
How to Contribute to Open Source Projects:
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  Before Contributing:                                           │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ 1. Read project documentation thoroughly               │   │
│  │ 2. Study coding style and conventions                  │   │
│  │ 3. Check existing issues and discussions               │   │
│  │ 4. Start with small contributions                      │   │
│  │ 5. Join mailing lists or chat channels                │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Good Contribution Practices:                                   │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Write clear commit messages                           │   │
│  │ • Include proper documentation                          │   │
│  │ • Test your changes thoroughly                          │   │
│  │ • Be responsive to feedback                             │   │
│  │ • Follow project's license requirements                │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Community Etiquette:                                           │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Be respectful and professional                        │   │
│  │ • Search before asking questions                        │   │
│  │ • Provide complete information in bug reports           │   │
│  │ • Give credit where credit is due                       │   │
│  │ • Be patient with review process                        │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🎯 Interview Questions

### **Common GNU/Licensing Interview Questions**

#### **Question 1: GPL Understanding**
```
Q: Explain the difference between GPL v2 and GPL v3, and why Linus Torvalds 
   chose to keep the Linux kernel under GPL v2.

Expected Answer:
- GPL v3 added anti-tivoization clauses (preventing hardware restrictions)
- Enhanced patent protection in v3
- Linus opposed v3's restrictions on hardware implementations
- Linux kernel remains GPL v2 "only" not "or later"
- Shows understanding of licensing politics and technical implications
```

#### **Question 2: Commercial Use**
```
Q: A company wants to modify GPL software and sell it. What are their 
   obligations under the GPL?

Expected Answer:
- Must provide source code to customers
- Must maintain GPL license on modifications
- Can charge for distribution and support
- Cannot add additional restrictions
- Must include copy of GPL license
```

#### **Question 3: License Compatibility**
```
Q: Can you combine MIT licensed code with GPL licensed code? What about 
   the reverse?

Expected Answer:
- MIT → GPL: Yes, MIT is compatible with GPL
- GPL → MIT: No, GPL cannot be relicensed as MIT
- GPL is "one-way compatible" with permissive licenses
- Resulting combination would be GPL licensed
```

#### **Question 4: Business Models**
```
Q: How does Red Hat make money from open source software?

Expected Answer:
- Support and maintenance subscriptions
- Training and certification services
- Consulting and custom development
- Enterprise features and management tools
- Long-term support guarantees
- Professional services around open source stack
```

---

## 🎯 Summary and Next Steps

### **Day 4 Accomplishments**

✅ **GNU and Licensing Mastery Achieved:**
- GNU Project history and philosophy understanding
- Four freedoms of free software comprehension
- GPL versions and copyleft mechanism mastery
- License comparison and business implications
- Practical license investigation skills
- Open source vs proprietary development models
- Community participation guidelines

### **Key Takeaways:**
```
Essential Concepts Mastered:
┌─────────────────────────────────────────────────────────────────┐
│ • Free Software = Freedom, not just free price                 │
│ • GPL ensures software freedom through copyleft                │
│ • Different licenses serve different purposes                  │
│ • Open source enables sustainable business models              │
│ • Community contribution requires understanding etiquette      │
│ • License compliance is crucial for businesses                 │
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