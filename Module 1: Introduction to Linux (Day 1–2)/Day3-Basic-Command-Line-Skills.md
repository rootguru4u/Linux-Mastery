# Day 3: Basic Command-Line Skills

---
**📚 Course:** rootguru Linux Classes  
**🌐 Website:** [www.rootguru.info](http://www.rootguru.info)  
**📖 Document:** Linux Fundamentals - Day 3 Command-Line Mastery Guide  
**🎯 Level:** Absolute Beginner  
**⏱️ Duration:** 4-5 hours  
**💻 Platform:** CentOS 7 / RHEL 7  
**👨‍🏫 Created by:** rootguru Team  

---

## 📖 Table of Contents

1. [Linux Filesystem Hierarchy Overview](#linux-filesystem-hierarchy-overview)
2. [Essential Navigation Commands](#essential-navigation-commands)
3. [Understanding Absolute vs Relative Paths](#understanding-absolute-vs-relative-paths)
4. [File and Directory Creation Operations](#file-and-directory-creation-operations)
5. [File Content Viewing Commands](#file-content-viewing-commands)
6. [Essential Utility Commands](#essential-utility-commands)
7. [Understanding Linux File Types](#understanding-linux-file-types)
8. [Mastering Wildcards and Pattern Matching](#mastering-wildcards-and-pattern-matching)
9. [Command-Line Efficiency Tips](#command-line-efficiency-tips)
10. [Practice Exercises](#practice-exercises)
11. [Interview Questions](#interview-questions)

---

## 🗂️ Linux Filesystem Hierarchy Overview

### **Understanding the Linux Directory Structure**

#### **Complete Filesystem Layout**
```
┌─────────────────────────────────────────────────────────────────┐
│                Linux Filesystem Hierarchy (FHS)                │
└─────────────────────────────────────────────────────────────────┘

/ (Root Directory) - The foundation of everything
├── bin/           # Essential user command binaries
│   ├── ls         # List directory contents
│   ├── cp         # Copy files and directories
│   ├── mv         # Move/rename files
│   ├── rm         # Remove files
│   └── cat        # Display file contents
├── boot/          # Boot loader files and kernel images
│   ├── grub2/     # GRUB bootloader configuration
│   └── vmlinuz-*  # Linux kernel files
├── dev/           # Device files (hardware access points)
│   ├── sda        # First SATA/SCSI disk
│   ├── tty1       # Virtual terminal 1
│   └── null       # Null device (data black hole)
├── etc/           # System-wide configuration files
│   ├── passwd     # User account information
│   ├── group      # Group definitions
│   ├── hosts      # Local hostname to IP mappings
│   └── fstab      # Filesystem mount table
├── home/          # User home directories
│   ├── user1/     # First user's personal space
│   ├── user2/     # Second user's personal space
│   └── sysadmin/  # System administrator's home
├── lib/           # Essential shared libraries
├── lib64/         # 64-bit shared libraries
├── media/         # Removable media mount points
├── mnt/           # Temporary mount points
├── opt/           # Optional software packages
├── proc/          # Virtual filesystem (process information)
├── root/          # Root user's home directory
├── run/           # Runtime data for running processes
├── sbin/          # Essential system binaries
│   ├── fdisk      # Disk partitioning utility
│   ├── mount      # Mount filesystems
│   └── iptables   # Firewall management
├── srv/           # Service data directories
├── sys/           # Virtual filesystem (system information)
├── tmp/           # Temporary files (cleared on reboot)
├── usr/           # Secondary hierarchy for user data
│   ├── bin/       # Non-essential user binaries
│   ├── lib/       # Libraries for /usr/bin programs
│   ├── local/     # Locally compiled software
│   └── share/     # Architecture-independent data
└── var/           # Variable data files
    ├── log/       # System and application log files
    ├── mail/      # User mailboxes
    ├── www/       # Web server document root
    └── tmp/       # Temporary files (preserved across reboots)
```

#### **Directory Purposes for Beginners**
```
🏠 User-Related Directories:
┌─────────────────────────────────────────────────────────────────┐
│ Directory │ Purpose                    │ Example Contents       │
├───────────┼────────────────────────────┼────────────────────────┤
│ /home     │ User personal directories  │ Documents, Downloads   │
│ /root     │ Root user's home          │ Admin scripts, configs │
│ /tmp      │ Temporary files           │ Browser cache, temp    │
└─────────────────────────────────────────────────────────────────┘

⚙️ System Configuration:
┌─────────────────────────────────────────────────────────────────┐
│ Directory │ Purpose                    │ Example Contents       │
├───────────┼────────────────────────────┼────────────────────────┤
│ /etc      │ System configuration      │ Network, user settings │
│ /boot     │ Boot files               │ Kernel, bootloader     │
│ /dev      │ Hardware devices         │ Disks, terminals       │
└─────────────────────────────────────────────────────────────────┘

🔧 Programs and Libraries:
┌─────────────────────────────────────────────────────────────────┐
│ Directory │ Purpose                    │ Example Contents       │
├───────────┼────────────────────────────┼────────────────────────┤
│ /bin      │ Essential commands        │ ls, cp, mv, rm         │
│ /sbin     │ System administration     │ mount, fdisk, iptables │
│ /usr/bin  │ User programs            │ firefox, vim, git      │
│ /lib      │ System libraries         │ Shared code libraries  │
└─────────────────────────────────────────────────────────────────┘

📊 Data and Logs:
┌─────────────────────────────────────────────────────────────────┐
│ Directory │ Purpose                    │ Example Contents       │
├───────────┼────────────────────────────┼────────────────────────┤
│ /var/log  │ System logs              │ Error logs, access logs│
│ /var/www  │ Web server files         │ HTML, PHP files        │
│ /opt      │ Optional software        │ Third-party packages   │
│ /srv      │ Service data             │ FTP, web service data  │
└─────────────────────────────────────────────────────────────────┘
```

#### **Memory Aid for Directory Structure**
```
🧠 Remember the Linux Filesystem:

Think of Linux filesystem like a city:
┌─────────────────────────────────────────────────────────────────┐
│ /          = City Hall (everything starts here)                │
│ /home      = Residential neighborhoods (where people live)     │
│ /bin       = Hardware store (essential tools everyone needs)   │
│ /etc       = City planning office (configuration and rules)    │
│ /var/log   = City records office (logs and documentation)      │
│ /tmp       = Public parking (temporary storage)                │
│ /dev       = Utility connections (water, electric, cable)      │
│ /boot      = Foundation (what the city is built on)           │
└─────────────────────────────────────────────────────────────────┘

Navigation Principle: "Everything starts at / and branches out"
```

---

## 🧭 Essential Navigation Commands

### **Mastering Filesystem Navigation**

#### **Core Navigation Commands**
```bash
# pwd - Print Working Directory
# Shows your current location in the filesystem
pwd
# Output: /home/sysadmin

# Why pwd is essential:
# - Always know where you are
# - Confirms your location before operations
# - Helps debug navigation issues
# - Essential for scripting

# cd - Change Directory
# Navigate to different locations
cd /home                    # Go to /home directory
cd ..                       # Go up one level (parent directory)
cd ../..                    # Go up two levels
cd ~                        # Go to your home directory
cd /                        # Go to root directory
cd -                        # Go back to previous directory

# cd usage patterns:
cd                          # No argument = go to home directory
cd Documents                # Relative path from current location
cd /etc/network            # Absolute path from root
cd ~/Downloads             # Tilde expansion to home directory

# ls - List directory contents
# View files and directories
ls                         # Basic listing
ls -l                      # Long format (detailed information)
ls -a                      # Show all files (including hidden)
ls -la                     # Long format + all files
ls -lah                    # Long format + all files + human readable
ls -lt                     # Sort by modification time
ls -lS                     # Sort by file size
ls -lr                     # Reverse sort order

# ls output explanation:
# -rw-r--r-- 1 user group 1024 Jan 15 10:30 file.txt
# │          │ │    │     │    │         │
# │          │ │    │     │    └─────────── modification time
# │          │ │    │     └──────────────── file size (bytes)
# │          │ │    └───────────────────── group ownership
# │          │ └────────────────────────── user ownership
# │          └─────────────────────────── number of links
# └────────────────────────────────────── file permissions

# tree - Visual directory structure
# Install if not available: sudo yum install tree
tree                       # Show directory tree from current location
tree /etc                  # Show tree structure of /etc
tree -d                    # Show only directories
tree -L 2                  # Limit depth to 2 levels
tree -a                    # Include hidden files
tree -I "*.tmp"           # Ignore files matching pattern

# Example tree output:
# .
# ├── Documents/
# │   ├── file1.txt
# │   └── projects/
# │       └── script.sh
# ├── Downloads/
# └── Pictures/
```

#### **Navigation Practice Patterns**
```bash
# Essential Navigation Workflow:

# 1. Always check where you are
pwd

# 2. See what's available
ls -la

# 3. Navigate with purpose
cd target_directory

# 4. Confirm your location
pwd

# 5. Explore the new location
ls -la

# Common Navigation Scenarios:

# Scenario 1: Exploring system directories
cd /etc                    # Go to configuration directory
ls -la | head -20         # Look at first 20 entries
cd network-scripts        # Go to network configs (if exists)
pwd                       # Confirm location
cd -                      # Go back to previous directory

# Scenario 2: Working in home directory
cd ~                      # Go to home directory
ls -la                    # See all files including hidden
mkdir practice            # Create practice directory
cd practice               # Enter practice directory
pwd                       # Confirm: /home/username/practice

# Scenario 3: System exploration
cd /var/log               # Go to log directory
ls -lt | head -10        # See 10 most recent log files
cd /usr/bin              # Go to user programs
ls | grep -i editor      # Find editors available

# Navigation Shortcuts:
cd                        # Quick home directory access
cd -                      # Toggle between two directories
pushd /etc && popd       # Save current dir, go to /etc, return
```

---

## 🛤️ Understanding Absolute vs Relative Paths

### **Path Types and Navigation Strategies**

#### **Absolute Paths - Starting from Root**
```
┌─────────────────────────────────────────────────────────────────┐
│                        Absolute Paths                          │
└─────────────────────────────────────────────────────────────────┘

Definition: Always start with / (root directory)
Advantage: Unambiguous - always refers to same location
Use Case: Scripts, configuration files, documentation

Examples:
/home/sysadmin/Documents/project1/readme.txt
/etc/network/interfaces
/var/log/messages
/usr/bin/firefox
/tmp/temporary-file.txt

Visual Representation:
/
├── home/
│   └── sysadmin/
│       └── Documents/
│           └── project1/
│               └── readme.txt ← /home/sysadmin/Documents/project1/readme.txt
├── etc/
│   └── network/
│       └── interfaces ← /etc/network/interfaces
└── var/
    └── log/
        └── messages ← /var/log/messages

Absolute Path Commands:
cd /home/sysadmin         # Always goes to sysadmin's home
ls /etc                   # Always lists /etc contents
cp /etc/hosts /tmp/       # Copy from /etc to /tmp
```

#### **Relative Paths - From Current Location**
```
┌─────────────────────────────────────────────────────────────────┐
│                        Relative Paths                          │
└─────────────────────────────────────────────────────────────────┘

Definition: Path relative to current working directory
Advantage: Shorter, more flexible for local operations
Use Case: Daily file operations, local navigation

Special Symbols:
.  = Current directory
.. = Parent directory (one level up)
~  = Home directory
-  = Previous directory

Current Location: /home/sysadmin/Documents

Relative Path Examples:
project1/readme.txt           → /home/sysadmin/Documents/project1/readme.txt
../Downloads/file.zip         → /home/sysadmin/Downloads/file.zip
../../etc/hosts              → /etc/hosts
~/Pictures/photo.jpg         → /home/sysadmin/Pictures/photo.jpg
./script.sh                  → /home/sysadmin/Documents/script.sh

Navigation Examples:
cd project1                  # Go to project1 subdirectory
cd ..                        # Go up to /home/sysadmin
cd ../Downloads              # Go to Downloads directory
cd ~/Desktop                 # Go to Desktop in home
cd -                         # Go to previous directory
```

#### **Path Conversion Examples**
```bash
# Understanding Path Relationships:

# Current directory: /home/sysadmin/Documents
pwd
# Output: /home/sysadmin/Documents

# Relative to Absolute Conversion:
ls project1/readme.txt       # Relative path
ls /home/sysadmin/Documents/project1/readme.txt  # Same file, absolute

# Different ways to reach the same file:
cd /home/sysadmin/Documents/project1    # Absolute path
cd ~/Documents/project1                  # Home directory relative
cd Documents/project1                    # Relative from /home/sysadmin

# Practice: Path Translation
# If you're in /home/sysadmin/Documents:
../Downloads/file.zip        # = /home/sysadmin/Downloads/file.zip
./project1/readme.txt        # = /home/sysadmin/Documents/project1/readme.txt
../../etc/hosts              # = /etc/hosts
~/Pictures/photo.jpg         # = /home/sysadmin/Pictures/photo.jpg

# Verification Commands:
realpath project1/readme.txt            # Shows absolute path
readlink -f ../Downloads/file.zip       # Resolves to absolute path
```

#### **When to Use Which Path Type**
```
Use Absolute Paths When:
✅ Writing scripts that run from different locations
✅ Documenting procedures for others
✅ Configuring system services
✅ Creating symbolic links
✅ Working with cron jobs
✅ Specifying paths in configuration files

Examples:
#!/bin/bash
LOG_FILE="/var/log/application.log"
CONFIG_FILE="/etc/myapp/config.conf"

Use Relative Paths When:
✅ Working within a project directory
✅ Daily file operations in current area
✅ Moving or copying nearby files
✅ Quick navigation between related directories
✅ Working with portable directory structures

Examples:
cd project-docs
cp readme.txt ../backup/
ls images/*.jpg
```

---

## 📁 File and Directory Creation Operations

### **Creating, Renaming, and Managing Files**

#### **File Creation Commands**
```bash
# touch - Create empty files or update timestamps
touch newfile.txt                    # Create single empty file
touch file1.txt file2.txt file3.txt  # Create multiple files
touch "file with spaces.txt"         # Handle spaces in names
touch /tmp/tempfile.txt              # Create file with absolute path

# touch with timestamp manipulation:
touch -t 202412250900.30 oldfile.txt  # Set specific timestamp
touch -r existing.txt newfile.txt     # Copy timestamp from existing file

# Why use touch:
# - Quick empty file creation
# - Update file modification times
# - Create placeholder files for scripts
# - Test file permissions

# Creating files with content:
echo "Hello World" > greeting.txt           # Create with content (overwrites)
echo "Additional line" >> greeting.txt      # Append to existing file
cat > document.txt << EOF                   # Create multi-line file
This is line 1
This is line 2
This is line 3
EOF

# Using text editors to create files:
vim newfile.txt                            # Create/edit with vim
nano simpler.txt                           # Create/edit with nano
```

#### **Directory Creation Commands**
```bash
# mkdir - Make directories
mkdir newdirectory                    # Create single directory
mkdir dir1 dir2 dir3                 # Create multiple directories
mkdir "directory with spaces"         # Handle spaces in names

# mkdir with parent creation:
mkdir -p projects/web/html           # Create entire path structure
mkdir -p backup/{daily,weekly,monthly}  # Create multiple subdirectories

# Directory creation with permissions:
mkdir -m 755 public_directory        # Create with specific permissions
mkdir -m 700 private_directory       # Create private directory

# Practical directory structures:
mkdir -p ~/projects/{personal,work,learning}
mkdir -p ~/documents/{contracts,invoices,receipts}
mkdir -p ~/scripts/{backup,monitoring,automation}

# Why use -p flag:
# - Creates parent directories if they don't exist
# - No error if directory already exists
# - Essential for scripting
```

#### **Moving and Renaming Operations**
```bash
# mv - Move and rename files/directories
# Note: mv is used for both moving AND renaming

# Renaming files:
mv oldname.txt newname.txt           # Rename file
mv "old name.txt" "new name.txt"     # Rename with spaces
mv script.py backup_script.py        # Rename with descriptive name

# Moving files:
mv file.txt /tmp/                    # Move to different directory
mv *.txt Documents/                  # Move all .txt files
mv file.txt ~/backup/renamed.txt     # Move and rename simultaneously

# Moving directories:
mv old_project_dir new_project_dir   # Rename directory
mv project1/ ~/archive/              # Move directory to archive

# Moving multiple items:
mv file1.txt file2.txt dir1/ destination/  # Move multiple items

# Interactive and safe moving:
mv -i source.txt destination.txt     # Interactive (ask before overwrite)
mv -n source.txt destination.txt     # Never overwrite existing
mv -v source.txt destination.txt     # Verbose (show what's happening)

# Common mv patterns:
# 1. Quick backup before editing:
mv important.conf important.conf.backup

# 2. Organize downloaded files:
mv ~/Downloads/*.pdf ~/Documents/PDFs/

# 3. Rename with timestamp:
mv logfile.txt "logfile_$(date +%Y%m%d).txt"
```

#### **Copying Operations**
```bash
# cp - Copy files and directories

# Basic file copying:
cp source.txt destination.txt        # Copy single file
cp source.txt /tmp/                  # Copy to different directory
cp *.txt backup/                     # Copy all .txt files

# Directory copying:
cp -r source_directory/ destination_directory/  # Recursive copy
cp -r ~/projects/ ~/backup/projects_backup/     # Backup entire project

# Preserving attributes:
cp -p source.txt destination.txt     # Preserve permissions and timestamps
cp -a source_directory/ backup/      # Archive mode (preserve everything)

# Interactive and safe copying:
cp -i source.txt destination.txt     # Interactive (ask before overwrite)
cp -n source.txt destination.txt     # Never overwrite existing
cp -v source.txt destination.txt     # Verbose output

# Useful cp combinations:
cp -rp ~/important_data/ /backup/    # Recursive with permissions preserved
cp -ruv source/ destination/         # Recursive, update only, verbose

# Creating backups with cp:
cp important.conf important.conf.$(date +%Y%m%d)  # Timestamped backup
cp -r project/ project_backup_$(date +%Y%m%d)/    # Directory backup
```

#### **Deletion Operations**
```bash
# rm - Remove files and directories
# ⚠️ CAUTION: rm permanently deletes files!

# File deletion:
rm file.txt                          # Delete single file
rm file1.txt file2.txt file3.txt     # Delete multiple files
rm *.tmp                             # Delete all .tmp files
rm /tmp/tempfile.txt                 # Delete with absolute path

# Safe deletion practices:
rm -i file.txt                       # Interactive (ask for confirmation)
rm -v file.txt                       # Verbose (show what's being deleted)

# Directory deletion:
rmdir empty_directory                # Remove empty directory only
rm -r directory_with_contents/       # Remove directory and all contents
rm -rf directory/                    # Force removal (no prompts)

# ⚠️ DANGEROUS COMMANDS - Use with extreme caution:
rm -rf /                             # NEVER DO THIS! Deletes everything
rm -rf /*                            # NEVER DO THIS! Deletes everything
rm -rf ~/                            # Deletes entire home directory

# Safe deletion patterns:
# 1. Always verify what you're deleting:
ls -la files_to_delete*              # Check what matches pattern
rm files_to_delete*                  # Then delete

# 2. Use trash instead of rm (if available):
# Install trash-cli: sudo yum install trash-cli
trash file.txt                      # Move to trash instead of delete
trash-list                          # List items in trash
trash-restore                       # Restore from trash

# 3. Create a safe rm alias:
alias rm='rm -i'                     # Always ask for confirmation

# Recovery note:
# Once rm deletes a file, it's very difficult to recover!
# Always backup important files before deletion.
```

---

## 👁️ File Content Viewing Commands

### **Reading and Examining File Contents**

#### **Basic Content Viewing**
```bash
# cat - Display entire file content
cat filename.txt                     # Display complete file
cat file1.txt file2.txt              # Display multiple files
cat -n filename.txt                  # Display with line numbers
cat -b filename.txt                  # Number only non-blank lines
cat -s filename.txt                  # Squeeze multiple blank lines

# Why use cat:
# - Quick view of small files
# - Combine multiple files
# - Create files from command line
# - Pipe content to other commands

# Cat usage examples:
cat /etc/hostname                    # View system hostname
cat /etc/os-release                  # View OS information
cat ~/.bashrc                       # View bash configuration

# Creating files with cat:
cat > newfile.txt                    # Type content, press Ctrl+D when done
cat >> existing.txt                  # Append to existing file
cat > config.txt << EOF              # Create multi-line file
setting1=value1
setting2=value2
setting3=value3
EOF
```

#### **Paginated Viewing for Large Files**
```bash
# less - Advanced file viewer (recommended)
less filename.txt                    # Open file in less viewer
less /var/log/messages               # View log files
less -N filename.txt                 # Show line numbers

# Less navigation keys:
# Space or f     = Next page
# b              = Previous page
# Enter or j     = Next line
# k              = Previous line
# g              = Go to beginning
# G              = Go to end
# /search_term   = Search forward
# ?search_term   = Search backward
# n              = Next search result
# N              = Previous search result
# q              = Quit

# Less advantages:
# - Memory efficient for large files
# - Powerful search capabilities
# - Can scroll both directions
# - Syntax highlighting for code files

# more - Simple file viewer
more filename.txt                    # Basic file pager
more +10 filename.txt               # Start at line 10

# More navigation:
# Space          = Next page
# Enter          = Next line
# q              = Quit
# /search_term   = Search

# When to use each:
# less: Default choice for file viewing
# more: Simple viewing, limited navigation needed
# cat: Quick display of small files
```

#### **Partial Content Viewing**
```bash
# head - Display first lines of file
head filename.txt                    # First 10 lines (default)
head -n 20 filename.txt             # First 20 lines
head -5 filename.txt                # First 5 lines
head -c 100 filename.txt            # First 100 characters

# Multiple files with head:
head -n 5 *.txt                     # First 5 lines of all .txt files
head -n 3 file1.txt file2.txt       # First 3 lines of specific files

# tail - Display last lines of file
tail filename.txt                    # Last 10 lines (default)
tail -n 20 filename.txt             # Last 20 lines
tail -5 filename.txt                # Last 5 lines
tail -c 100 filename.txt            # Last 100 characters

# Real-time file monitoring:
tail -f /var/log/messages           # Follow file (watch new additions)
tail -f -n 50 /var/log/httpd/access_log  # Follow last 50 lines

# Why tail -f is powerful:
# - Monitor log files in real-time
# - Watch application output
# - Debug running processes
# - Monitor file changes

# Practical viewing combinations:
head -n 1 /etc/passwd               # See first user entry
tail -n 1 /etc/passwd               # See last user entry
head -n 20 /var/log/messages | tail -n 10  # Lines 11-20 of log file

# File content statistics:
wc filename.txt                      # Word count (lines, words, characters)
wc -l filename.txt                   # Count lines only
wc -w filename.txt                   # Count words only
wc -c filename.txt                   # Count characters only
```

#### **Content Search and Analysis**
```bash
# grep - Search within files
grep "search_term" filename.txt      # Basic search
grep -i "search_term" filename.txt   # Case-insensitive search
grep -n "search_term" filename.txt   # Show line numbers
grep -v "exclude_term" filename.txt  # Show lines NOT containing term

# Powerful grep examples:
grep "error" /var/log/messages       # Find errors in log file
grep -r "TODO" ~/projects/           # Recursively search for TODO comments
grep -c "warning" logfile.txt        # Count occurrences
grep -A 3 -B 3 "error" log.txt      # Show 3 lines before and after match

# File type identification:
file filename.txt                    # Identify file type
file *                               # Check all files in directory
file /bin/ls                         # Check binary file type

# Content comparison:
diff file1.txt file2.txt             # Compare two files
diff -u file1.txt file2.txt          # Unified diff format
cmp file1.txt file2.txt              # Binary comparison

# Advanced content viewing:
strings binary_file                  # Extract readable strings from binary
hexdump -C filename.txt              # Hexadecimal dump of file
od -c filename.txt                   # Octal dump showing characters
```

---

## 🛠️ Essential Utility Commands

### **Command-Line Productivity Tools**

#### **Screen and Session Management**
```bash
# clear - Clear terminal screen
clear                                # Clean slate for better visibility

# Why clear is useful:
# - Remove clutter from terminal
# - Start fresh for new tasks
# - Improve focus and readability
# - Clean up before screenshots

# Alternative screen clearing:
Ctrl + L                            # Keyboard shortcut (same as clear)
printf '\033[2J\033[H'              # Direct terminal escape sequence

# Screen management tips:
# - Use clear before important operations
# - Clear screen when sharing terminal
# - Combine with other commands: clear && ls -la
```

#### **Command History Management**
```bash
# history - View command history
history                             # Show all previous commands
history 20                          # Show last 20 commands
history | grep "search_term"        # Search command history
history | tail -10                  # Last 10 commands

# History navigation:
!!                                  # Repeat last command
!n                                  # Execute command number n from history
!string                             # Execute last command starting with string
!?string?                           # Execute last command containing string

# History editing:
^old^new                            # Replace 'old' with 'new' in last command
!:0                                 # First word of last command
!:1                                 # Second word of last command
!:$                                 # Last word of last command

# Practical history examples:
!vim                                # Run last vim command
history | grep "cd"                 # Find all directory changes
!!                                  # Repeat last command (useful for sudo)

# History configuration:
export HISTSIZE=1000                # Number of commands in memory
export HISTFILESIZE=2000            # Number of commands in history file
export HISTCONTROL=ignoredups       # Ignore duplicate commands

# History file management:
~/.bash_history                     # Location of history file
history -c                          # Clear current session history
history -w                          # Write current session to history file
```

#### **Command Aliases and Shortcuts**
```bash
# alias - Create command shortcuts
alias ll='ls -la'                   # Create ll shortcut
alias la='ls -A'                    # List all except . and ..
alias l='ls -CF'                    # Classify files by type
alias ..='cd ..'                    # Quick parent directory access
alias ...='cd ../..'                # Quick grandparent access

# Useful aliases for beginners:
alias grep='grep --color=auto'      # Colorize grep output
alias cp='cp -i'                    # Interactive copy (ask before overwrite)
alias mv='mv -i'                    # Interactive move
alias rm='rm -i'                    # Interactive remove (safety)
alias df='df -h'                    # Human-readable disk usage
alias free='free -h'                # Human-readable memory usage

# System-specific aliases:
alias update='sudo yum update'      # Quick system update
alias install='sudo yum install'    # Quick package installation
alias search='yum search'           # Search for packages

# Viewing and managing aliases:
alias                               # List all current aliases
unalias ll                          # Remove specific alias
unalias -a                          # Remove all aliases

# Making aliases permanent:
echo "alias ll='ls -la'" >> ~/.bashrc        # Add to bash configuration
source ~/.bashrc                             # Reload configuration

# Advanced alias examples:
alias backup='cp -r ~/important ~/backup/$(date +%Y%m%d)'
alias myip='curl ifconfig.me'               # Get public IP address
alias ports='netstat -tuln'                # Show listening ports
```

#### **Help and Information Commands**
```bash
# man - Manual pages (comprehensive documentation)
man ls                              # Complete manual for ls command
man cp                              # Complete manual for cp command
man man                             # Manual for the man command itself

# Man page navigation:
# Space              = Next page
# b                  = Previous page
# /search_term       = Search forward
# n                  = Next search result
# q                  = Quit

# Man page sections:
man 1 passwd                        # User commands
man 5 passwd                        # File formats (/etc/passwd format)
man 8 mount                         # System administration commands

# which - Locate command executable
which ls                            # Shows: /bin/ls
which python                        # Shows: /usr/bin/python
which firefox                       # Shows: /usr/bin/firefox

# Why which is important:
# - Verify command exists
# - Find exact location of programs
# - Debug PATH issues
# - Understand command sources

# whereis - Locate binary, source, and manual files
whereis ls                          # Binary, source, and manual locations
whereis -b ls                       # Binary location only
whereis -m ls                       # Manual location only

# type - Display command type and location
type ls                             # Shows if command is alias, function, or binary
type -a ls                          # Show all locations
type cd                             # Shows: cd is a shell builtin

# info - Info documents (alternative to man)
info ls                             # Info documentation for ls
info coreutils                      # Info for core utilities

# Getting quick help:
ls --help                           # Quick help for ls
cp --help                           # Quick help for cp
grep --help | less                  # Paginated help display

# Command discovery:
apropos copy                        # Find commands related to copying
apropos network                     # Find network-related commands
whatis ls                           # Brief description of ls command
```

#### **System Information Commands**
```bash
# Date and time:
date                                # Current date and time
date +%Y-%m-%d                     # Formatted date: 2024-12-25
date +%H:%M:%S                     # Current time: 14:30:45

# System information:
whoami                              # Current username
id                                  # User and group IDs
groups                              # Groups you belong to
uptime                              # System uptime and load
uname -a                           # Complete system information

# Process information:
ps                                  # Current processes
ps aux                              # All processes with details
top                                 # Real-time process viewer
jobs                                # Current background jobs

# Disk and memory:
df -h                               # Disk usage (human readable)
du -h                               # Directory usage
free -h                             # Memory usage
lscpu                               # CPU information

# Network information:
hostname                            # System hostname
hostname -I                         # IP addresses
ip addr show                        # Network interface details
```

---

## 📄 Understanding Linux File Types

### **Comprehensive File Type Classification**

#### **Linux File Type System**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Linux File Types Overview                   │
└─────────────────────────────────────────────────────────────────┘

Linux treats everything as a file, but distinguishes these types:

1. Regular Files        (-)  # Normal files with data
2. Directories          (d)  # Containers for other files
3. Symbolic Links       (l)  # Shortcuts to other files
4. Character Devices    (c)  # Character-based hardware
5. Block Devices        (b)  # Block-based hardware
6. Named Pipes (FIFOs)  (p)  # Inter-process communication
7. Sockets             (s)  # Network/IPC communication

File Type Identification in ls -l output:
┌─────────────────────────────────────────────────────────────────┐
│ -rw-r--r--  1 user group 1024 Jan 15 file.txt    (Regular)     │
│ drwxr-xr-x  2 user group 4096 Jan 15 docs/       (Directory)   │
│ lrwxrwxrwx  1 user group   10 Jan 15 link.txt    (Symlink)     │
│ crw-rw-rw-  1 root root  1, 3 Jan 15 /dev/null   (Char Device) │
│ brw-rw----  1 root disk  8, 0 Jan 15 /dev/sda    (Block Device)│
│ prw-r--r--  1 user group    0 Jan 15 mypipe      (Named Pipe)  │
│ srwxrwxrwx  1 user group    0 Jan 15 socket      (Socket)      │
└─────────────────────────────────────────────────────────────────┘
   ↑
   First character indicates file type
```

#### **Regular Files - Standard Data Files**
```bash
# Regular Files (-) - Most common file type
# Contains data: text, binary, executable, media, etc.

# Identifying regular files:
ls -l | grep "^-"                   # Show only regular files
file filename.txt                   # Determine specific file type

# Examples of regular files:
ls -l /etc/passwd                   # Text configuration file
ls -l /bin/ls                       # Binary executable file
ls -l image.jpg                     # Binary media file
ls -l script.sh                     # Text script file

# Regular file subtypes (determined by content):
file /etc/passwd                    # ASCII text
file /bin/ls                        # ELF 64-bit LSB executable
file image.jpg                      # JPEG image data
file archive.tar.gz                 # gzip compressed data

# Creating regular files:
touch newfile.txt                   # Empty regular file
echo "content" > file.txt           # Text file with content
cp /bin/ls ./ls_copy               # Binary file copy

# Regular file characteristics:
# - Contains actual data or program code
# - Can be read, written, executed (with permissions)
# - Size reflects actual content size
# - Most files you work with daily are regular files
```

#### **Directories - File Containers**
```bash
# Directories (d) - Special files that contain other files
# Act as containers organizing the filesystem

# Identifying directories:
ls -l | grep "^d"                   # Show only directories
ls -ld directory_name              # Show directory info (not contents)

# Directory examples:
ls -ld /home                        # User home directories
ls -ld ~/Documents                  # Personal documents folder
ls -ld /etc                         # System configuration directory

# Directory operations:
mkdir new_directory                 # Create directory
rmdir empty_directory              # Remove empty directory
rm -r directory_with_files         # Remove directory and contents

# Directory characteristics:
# - Contains entries pointing to other files
# - Size usually 4096 bytes (default block size)
# - Requires execute permission to enter
# - Requires read permission to list contents
# - Requires write permission to create/delete files inside

# Special directories:
ls -la                              # Shows . (current) and .. (parent)
.                                   # Current directory
..                                  # Parent directory
~                                   # Home directory shortcut
```

#### **Symbolic Links - File Shortcuts**
```bash
# Symbolic Links (l) - Pointers to other files or directories
# Like shortcuts in Windows or aliases in macOS

# Creating symbolic links:
ln -s /path/to/original linkname    # Create symbolic link
ln -s /etc/passwd passwd_link       # Link to system file
ln -s /var/log/messages log_link    # Link to log file
ln -s ../Documents/file.txt shortcut.txt  # Relative link

# Viewing symbolic links:
ls -l | grep "^l"                   # Show only symbolic links
ls -la                              # Links show target with ->

# Example symbolic link display:
# lrwxrwxrwx 1 user group 11 Jan 15 link.txt -> /etc/passwd
#                                     ↑
#                                Points to target

# Working with symbolic links:
readlink linkname                   # Show what link points to
readlink -f linkname               # Show absolute path of target
file linkname                      # Shows "symbolic link to..."

# Symbolic link characteristics:
# - Size is the length of the target path string
# - Can link to files or directories
# - Can cross filesystem boundaries
# - Becomes "broken" if target is deleted
# - Can create circular references (link to link)

# Broken link identification:
ls -l | grep " -> "                 # Find all symbolic links
find . -type l -exec test ! -e {} \; -print  # Find broken links

# Practical symbolic link uses:
ln -s /var/www/html ~/website      # Quick access to web directory
ln -s /etc/httpd/conf/httpd.conf ~/web-config  # Easy config access
ln -s /usr/bin/python3 /usr/local/bin/python   # Version management
```

#### **Device Files - Hardware Access Points**
```bash
# Character Devices (c) - Stream-oriented hardware
# Data flows in character streams (keyboards, terminals, serial ports)

# Common character devices:
ls -l /dev/tty*                     # Terminal devices
ls -l /dev/null                     # Null device (data black hole)
ls -l /dev/zero                     # Zero device (infinite zeros)
ls -l /dev/random                   # Random number generator

# Character device examples:
ls -l /dev/null
# crw-rw-rw- 1 root root 1, 3 Jan 15 /dev/null

# Using character devices:
echo "test" > /dev/null             # Send data to nowhere
cat /dev/zero | head -c 10          # Get 10 zero bytes
cat /dev/random | head -c 10        # Get 10 random bytes

# Block Devices (b) - Block-oriented hardware
# Data handled in fixed-size blocks (hard drives, USB drives)

# Common block devices:
ls -l /dev/sd*                      # SATA/SCSI disk devices
ls -l /dev/loop*                    # Loop devices
ls -l /dev/mapper/*                 # Device mapper devices

# Block device examples:
ls -l /dev/sda
# brw-rw---- 1 root disk 8, 0 Jan 15 /dev/sda

# Block device information:
lsblk                               # List block devices in tree format
fdisk -l /dev/sda                   # Show partition information
df /dev/sda1                        # Show filesystem usage

# Device file characteristics:
# - Provide interface to hardware
# - Major and minor numbers identify device type
# - Permissions control access to hardware
# - Created by system, not users
```

#### **Named Pipes and Sockets**
```bash
# Named Pipes (p) - Inter-process communication
# Also called FIFOs (First In, First Out)

# Creating named pipes:
mkfifo mypipe                       # Create named pipe
ls -l mypipe
# prw-r--r-- 1 user group 0 Jan 15 mypipe

# Using named pipes:
# Terminal 1:
echo "Hello from process 1" > mypipe

# Terminal 2:
cat < mypipe                        # Receives: Hello from process 1

# Named pipe characteristics:
# - Enables communication between processes
# - Data written by one process, read by another
# - Blocking operations (writers wait for readers)
# - No permanent data storage

# Sockets (s) - Network and local communication
# Used for network connections and local IPC

# Socket examples:
ls -l /tmp/.X11-unix/              # X11 display sockets
ls -l /var/run/                    # System service sockets

# Socket display example:
# srwxrwxrwx 1 user group 0 Jan 15 socket_name

# Socket characteristics:
# - Enable network communication
# - Support both local and remote connections
# - Used by web servers, databases, etc.
# - Created by applications, not directly by users

# Finding different file types:
find /dev -type c | head -5         # Character devices
find /dev -type b | head -5         # Block devices
find /tmp -type s 2>/dev/null       # Sockets
find /tmp -type p 2>/dev/null       # Named pipes
```

---

## 🎯 Mastering Wildcards and Pattern Matching

### **Advanced Pattern Matching for Efficient File Operations**

#### **Asterisk (*) - Match Any Characters**
```bash
# * (asterisk) - Matches zero or more characters

# Basic asterisk usage:
ls *.txt                            # All files ending with .txt
ls file*                            # All files starting with "file"
ls *report*                         # All files containing "report"
ls *                                # All files (same as ls)

# Multiple asterisks:
ls *.log.*                          # Files like: app.log.1, error.log.old
ls *test*.py                        # Python files containing "test"
ls data*2024*                       # Files starting with "data" and containing "2024"

# Practical asterisk examples:
cp *.txt backup/                    # Copy all text files to backup
mv *.tmp /tmp/                      # Move all temporary files
rm *.bak                            # Delete all backup files
ls -la *.conf                       # List all configuration files

# Directory navigation with asterisk:
cd */                               # Enter first directory found
ls */                               # List all subdirectories
echo */                             # Show directory names

# Asterisk limitations and gotchas:
ls *                                # Doesn't match hidden files (.files)
ls .*                               # Matches hidden files only
ls * .*                             # Matches both visible and hidden files

# Complex asterisk patterns:
ls project_*_final.*                # Matches: project_web_final.zip
mv *_backup_* archive/              # Move all backup files
find . -name "*.log*" -type f       # Find all log-related files
```

#### **Question Mark (?) - Match Single Character**
```bash
# ? (question mark) - Matches exactly one character

# Basic question mark usage:
ls file?.txt                        # Matches: file1.txt, filea.txt, file_.txt
ls test??.py                        # Matches: test01.py, testAB.py, test__.py
ls image?.jpg                       # Matches: image1.jpg, imagex.jpg

# Question mark vs asterisk:
ls file*.txt                        # Matches: file.txt, file123.txt, filename.txt
ls file?.txt                        # Matches: file1.txt, filex.txt (single char only)

# Practical question mark examples:
ls log?.txt                         # Daily logs: log1.txt, log2.txt, etc.
mv test?.bak archive/               # Move single-digit test backups
cp data??.csv reports/              # Copy two-digit data files

# Multiple question marks:
ls ????-??-??.log                   # Date format: 2024-12-25.log
ls user???.conf                     # Three-character user configs
mv backup_??_*.tar.gz old_backups/  # Specific backup patterns

# Question mark in different contexts:
find . -name "temp?.txt"            # Find temp files with single character
grep "error?" logfile.txt           # In grep, ? means "zero or one occurrence"
ls chapter?.pdf                     # Book chapters: chapter1.pdf, chapter9.pdf
```

#### **Square Brackets ([]) - Character Sets and Ranges**
```bash
# [] (square brackets) - Match any single character from the set

# Character sets:
ls file[123].txt                    # Matches: file1.txt, file2.txt, file3.txt
ls image[abc].jpg                   # Matches: imagea.jpg, imageb.jpg, imagec.jpg
ls log[0-9].txt                     # Matches: log0.txt through log9.txt

# Character ranges:
ls [a-z]*.txt                       # Files starting with lowercase letter
ls [A-Z]*.pdf                       # Files starting with uppercase letter
ls [0-9][0-9].log                   # Two-digit numbered logs: 01.log, 99.log

# Mixed ranges and sets:
ls [a-zA-Z]*.conf                   # Files starting with any letter
ls file[0-9a-f].txt                 # Files with digit or hex a-f
ls [aeiou]*.txt                     # Files starting with vowels

# Negation with brackets:
ls [!0-9]*.txt                      # Files NOT starting with digit
ls file[!abc].txt                   # file + any char except a, b, or c
ls [!.]*                            # All files NOT starting with dot

# Advanced bracket patterns:
ls chapter[1-9].pdf                 # Chapters 1-9 (excludes 0)
ls backup[0-9][0-9][0-9].tar        # Three-digit backup numbers
ls test[A-Za-z][0-9].py             # test + letter + digit + .py

# Practical bracket examples:
mv [Tt]emp* /tmp/                   # Move files starting with Temp or temp
ls *[Bb]ackup*                      # Files containing Backup or backup
cp section[1-5].docx final/         # Copy sections 1 through 5
rm old[0-9][0-9].log               # Remove two-digit old logs

# Bracket special characters:
ls file[*].txt                      # Literal asterisk in filename
ls file[?].txt                      # Literal question mark in filename
ls file[\[\]].txt                   # Literal brackets in filename
```

#### **Advanced Wildcard Combinations**
```bash
# Combining multiple wildcards for powerful patterns:

# Complex file selection:
ls *[0-9]*.log                      # Files containing digits with .log extension
mv *test*[0-9].tmp archive/         # Test files ending with digit and .tmp
cp project[1-5]_*final*.zip backup/ # Specific project finals

# Date-based patterns:
ls 202[0-9]-[01][0-9]-[0-3][0-9].log    # Date format logs: 2020-12-25.log
mv backup_[0-9][0-9][0-9][0-9]*.tar.gz old/  # Year-based backups

# Mixed extension patterns:
ls *.{txt,log,conf}                 # Multiple extensions (brace expansion)
mv *.[Ll]og /var/log/              # Files ending with .log or .Log
cp *.[0-9] archive/                # Files ending with single digit

# Directory and file combinations:
ls */README*                        # README files in subdirectories
find . -name "*[Tt]est*" -type f    # Test files (case variations)
rm -r temp[0-9]*/                   # Remove numbered temp directories

# Exclusion patterns:
ls *[!~]                           # All files not ending with ~
mv *[!.bak] active/                # Move all except .bak files
ls [!.]*                           # All files not starting with dot

# Performance and safety considerations:
echo pattern*                      # Test pattern before using
ls -1 pattern* | wc -l            # Count matches
set -f; ls *; set +f              # Disable/enable globbing temporarily
```

#### **Wildcard Best Practices and Gotchas**
```bash
# Common wildcard mistakes and solutions:

# Problem: Accidental command expansion
rm * .txt                          # DANGEROUS: Removes all files + .txt
rm *.txt                           # CORRECT: Removes only .txt files

# Problem: Hidden files not matching
ls *                               # Doesn't show .hidden files
ls .* *                            # Shows both hidden and visible files
ls -A                              # Better: shows all except . and ..

# Problem: No matches found
ls *.xyz                           # Error if no .xyz files exist
ls *.xyz 2>/dev/null || echo "No .xyz files found"  # Handle gracefully

# Safe wildcard practices:
# 1. Always test patterns first:
echo *.txt                         # Preview what will be matched
ls *.txt                           # Verify before operations

# 2. Use quotes to prevent expansion:
grep "*.txt" file.txt              # Search for literal *.txt
echo "*.txt"                       # Print literal *.txt

# 3. Escape wildcards when needed:
ls \*.txt                          # Look for file literally named *.txt
touch "file*.txt"                  # Create file with * in name
ls "file*.txt"                     # Access file with * in name

# 4. Handle edge cases:
shopt -s nullglob                  # Empty expansion if no matches
shopt -s dotglob                   # Include hidden files in *
shopt -u nullglob dotglob          # Reset to defaults

# Advanced wildcard examples:
# Find files modified in last 24 hours with pattern:
find . -name "*.log" -mtime -1

# Move files matching complex patterns:
for file in *test*[0-9].{py,sh}; do
    [ -f "$file" ] && mv "$file" archive/
done

# Backup files with timestamp:
for file in *.conf; do
    [ -f "$file" ] && cp "$file" "${file%.conf}_$(date +%Y%m%d).conf.bak"
done
```

---

## ⚡ Command-Line Efficiency Tips

### **Professional Terminal Productivity Techniques**

#### **Keyboard Shortcuts for Speed**
```bash
# Essential Terminal Navigation Shortcuts:

# Cursor Movement:
Ctrl + A                            # Move to beginning of line
Ctrl + E                            # Move to end of line
Ctrl + F                            # Move forward one character
Ctrl + B                            # Move backward one character
Alt + F                             # Move forward one word
Alt + B                             # Move backward one word

# Text Editing:
Ctrl + U                            # Delete from cursor to beginning of line
Ctrl + K                            # Delete from cursor to end of line
Ctrl + W                            # Delete word before cursor
Alt + D                             # Delete word after cursor
Ctrl + Y                            # Paste (yank) last deleted text
Ctrl + T                            # Transpose characters

# Command Control:
Ctrl + C                            # Cancel current command
Ctrl + Z                            # Suspend current command (send to background)
Ctrl + D                            # End of file / Exit shell
Ctrl + L                            # Clear screen (same as clear command)

# History Navigation:
Ctrl + R                            # Reverse search through history
Ctrl + P                            # Previous command (same as Up arrow)
Ctrl + N                            # Next command (same as Down arrow)
```

#### **Tab Completion Mastery**
```bash
# Tab Completion - Your Best Friend for Speed and Accuracy

# File and Directory Completion:
ls Doc[TAB]                         # Completes to Documents/
cd /etc/net[TAB]                    # Completes to /etc/network-scripts/
vim ~/.bash[TAB]                    # Completes to ~/.bashrc

# Command Completion:
fire[TAB]                           # Completes to firefox
sys[TAB][TAB]                       # Shows all commands starting with 'sys'
yum ins[TAB]                        # Completes to 'yum install'

# Double-Tab for Options:
ls -[TAB][TAB]                      # Shows all ls options
git [TAB][TAB]                      # Shows all git subcommands
ssh [TAB][TAB]                      # Shows available hosts (from config)

# Advanced Tab Completion:
# Configure programmable completion (bash-completion package)
sudo yum install bash-completion

# After installation, enjoy enhanced completion for:
systemctl st[TAB]                   # Completes systemctl commands
ssh user@[TAB]                      # Completes known hosts
git checkout [TAB]                  # Completes branch names

# Tab Completion Best Practices:
# 1. Use tab liberally - prevents typos
# 2. Double-tab to see options when stuck
# 3. Works with paths, commands, and arguments
# 4. Case-sensitive - match the actual case
```

#### **Command Chaining and Redirection**
```bash
# Command Chaining - Execute Multiple Commands

# Sequential Execution (;):
cd /tmp; ls -la; pwd                # Execute all commands in sequence
mkdir test; cd test; touch file.txt # Create, enter, and create file

# Conditional Execution (&&):
cd /tmp && ls -la                   # Second command only if first succeeds
make && make install                # Common pattern for compilation
ping -c 1 google.com && echo "Internet is working"

# Alternative Execution (||):
cd /nonexistent || echo "Directory not found"  # Second if first fails
which firefox || yum install firefox          # Install if not found

# Background Execution (&):
firefox &                           # Run in background, return to terminal
tail -f /var/log/messages &         # Monitor logs in background
jobs                                # Show background jobs
fg                                  # Bring last job to foreground

# Redirection for Efficiency:
ls -la > filelist.txt               # Save output to file
grep "error" logfile.txt > errors.txt  # Save search results
command 2> errors.log               # Redirect errors to file
command > output.txt 2>&1           # Redirect both output and errors
command &> all_output.txt           # Shorter way to redirect everything
```

#### **Advanced Command-Line Techniques**
```bash
# Brace Expansion - Generate Multiple Arguments:
mkdir {backup,archive,temp}         # Create three directories
cp file.txt{,.backup}              # Copy file.txt to file.txt.backup
mv project{_old,_new}               # Rename project_old to project_new

# Advanced brace patterns:
mkdir project/{src,docs,tests}/{python,java}  # Nested directory structure
touch file_{1..10}.txt              # Create file_1.txt through file_10.txt
echo {a..z}                         # Print alphabet
echo {01..12}                       # Print 01 through 12 (zero-padded)

# Command Substitution - Use Command Output as Input:
echo "Today is $(date)"             # Modern syntax
echo "Today is `date`"              # Old syntax (still works)
cd $(dirname /path/to/file.txt)     # Go to directory containing file
vi $(which firefox)                 # Edit the firefox executable

# Process Substitution:
diff <(ls dir1) <(ls dir2)          # Compare directory listings
grep pattern <(cat file1 file2)     # Search in combined files

# Parameter Expansion - Advanced Variable Manipulation:
filename="document.txt"
echo ${filename%.txt}.backup        # Outputs: document.backup
echo ${filename#doc}                # Outputs: ument.txt
echo ${filename/txt/pdf}            # Outputs: document.pdf

# History Expansion - Reuse Previous Commands:
!!                                  # Last command
!n                                  # Command number n from history
!string                             # Last command starting with string
^old^new                            # Replace 'old' with 'new' in last command
!:1                                 # First argument of last command
!:$                                 # Last argument of last command
!:1-3                               # Arguments 1 through 3 of last command
```

#### **Environment Customization**
```bash
# Prompt Customization:
export PS1='\u@\h:\w\$ '            # User@host:directory$
export PS1='[\t] \u@\h:\w\$ '       # [time] user@host:directory$
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '  # Colored prompt

# Environment Variables:
export EDITOR=vim                   # Default text editor
export BROWSER=firefox              # Default web browser
export PAGER=less                   # Default pager
export HISTSIZE=10000               # Command history size

# Path Management:
export PATH=$PATH:/opt/custom/bin   # Add directory to PATH
export PATH=/usr/local/bin:$PATH    # Prepend to PATH (higher priority)
echo $PATH | tr ':' '\n'           # Display PATH directories one per line

# Useful Functions in ~/.bashrc:
# Quick directory creation and navigation:
mkcd() { mkdir -p "$1" && cd "$1"; }

# Quick file backup:
backup() { cp "$1"{,.backup.$(date +%Y%m%d)}; }

# Search and replace in files:
replace() { sed -i "s/$1/$2/g" "$3"; }

# Find large files:
bigfiles() { find . -type f -size +${1:-100M} -exec ls -lh {} \; | sort -k5 -hr; }

# Source the configuration:
source ~/.bashrc                    # Reload configuration
```

---

## 🏋️ Practice Exercises

### **Hands-On Command-Line Mastery**

#### **Exercise 1: Filesystem Navigation Mastery**
```bash
# 🎯 Exercise 1: Complete Navigation Challenge
# Master navigation and path understanding

# Part A: Basic Navigation
# Start from your home directory
cd ~
pwd                                 # Should show /home/username

# Navigate to root and explore
cd /
ls -la
cd etc
pwd                                 # Should show /etc
cd ..
pwd                                 # Should show /

# Use different navigation methods
cd ~                                # Home directory
cd /var/log                         # Absolute path
cd ../..                            # Relative path (should be at /)
cd -                                # Previous directory (/var/log)
cd ~/Documents                      # Home-relative path

# Part B: Path Understanding Challenge
# Create this directory structure and practice navigation:
mkdir -p ~/practice/day3/{docs,scripts,logs}/{2024,2023,archive}

# Navigate using different path types:
cd ~/practice/day3/docs/2024        # Absolute with tilde
cd ../../scripts/archive            # Relative with ..
cd ~/practice/day3/logs             # Back to absolute
cd ../../../                       # Relative to practice directory

# Verification commands:
pwd                                 # Confirm location
ls -la                              # See contents
tree ~/practice                     # Visual structure (if tree installed)

✅ Expected Results:
□ Comfortable navigating with cd, pwd, ls
□ Understanding of absolute vs relative paths
□ Ability to move up/down directory hierarchy
□ Quick navigation using shortcuts (cd -, cd ~, cd ..)
```

#### **Exercise 2: File Operations Workshop**
```bash
# 🎯 Exercise 2: File and Directory Management
# Master creating, moving, copying, and deleting

# Setup: Create practice environment
cd ~
mkdir -p file_workshop/{originals,backups,archive,temp}
cd file_workshop

# Part A: File Creation
# Create various types of files
touch simple.txt
echo "This is a test file" > content.txt
echo -e "Line 1\nLine 2\nLine 3" > multiline.txt

# Create files with different extensions
touch document.pdf report.docx data.csv script.py config.conf

# Create files with numbers and patterns
touch file{1..5}.txt
touch log_{01..12}_2024.log
touch backup_$(date +%Y%m%d).tar.gz

# Part B: Directory Operations
mkdir {projects,documents,media}/{work,personal}
mkdir temp_{$(date +%m),$(date +%d)}

# Part C: Moving and Renaming
# Rename files
mv simple.txt renamed_simple.txt
mv content.txt originals/

# Move multiple files
mv *.pdf *.docx documents/work/
mv *.csv *.py projects/personal/

# Move with renaming
mv multiline.txt originals/renamed_multiline.txt

# Part D: Copying Operations
# Basic copying
cp originals/content.txt backups/
cp -r documents/ backups/documents_backup/

# Copy with rename
cp renamed_simple.txt archive/archived_simple.txt

# Copy multiple files
cp *.log temp/
cp projects/personal/* archive/

# Part E: Safe Deletion
# View before deleting
ls -la temp/
rm -i temp/*.log                    # Interactive deletion

# Remove empty directories
rmdir temp_*

# Clean up workspace
ls -la                              # Review what's left
rm -rf temp/                        # Remove temp directory

✅ Expected Results:
□ Files created with touch and echo
□ Directory structure properly organized
□ Files moved and renamed correctly
□ Backups created successfully
□ Safe deletion practices demonstrated
```

#### **Exercise 3: File Content and Viewing Mastery**
```bash
# 🎯 Exercise 3: Content Viewing and Analysis
# Master all file viewing commands

# Setup: Create test files with different content
cd ~/file_workshop
mkdir content_practice
cd content_practice

# Create sample files for practice
echo "This is a single line file" > single_line.txt

cat > multi_line.txt << EOF
Line 1: Introduction
Line 2: Content begins here
Line 3: More content
Line 4: Important information
Line 5: Data section
Line 6: Additional details
Line 7: More data
Line 8: Further information
Line 9: Near the end
Line 10: Conclusion
EOF

# Create a large file for practice
seq 1 100 > numbers.txt

# Create a log-like file
cat > sample.log << EOF
2024-01-01 10:00:01 INFO Application started
2024-01-01 10:00:02 DEBUG Loading configuration
2024-01-01 10:00:03 INFO Configuration loaded successfully
2024-01-01 10:00:04 WARNING Connection timeout
2024-01-01 10:00:05 ERROR Failed to connect to database
2024-01-01 10:00:06 INFO Retrying connection
2024-01-01 10:00:07 INFO Connected successfully
2024-01-01 10:00:08 DEBUG Processing request
2024-01-01 10:00:09 INFO Request processed
2024-01-01 10:00:10 INFO Application running normally
EOF

# Part A: Basic Content Viewing
cat single_line.txt               # View small file
cat multi_line.txt               # View multi-line file
cat -n multi_line.txt            # View with line numbers

# Part B: Paginated Viewing
less numbers.txt                 # Practice navigation (Space, b, g, G, q)
more multi_line.txt              # Simple pager
less sample.log                  # Practice searching (/ERROR, n, N)

# Part C: Partial Content Viewing
head multi_line.txt              # First 10 lines
head -n 5 multi_line.txt         # First 5 lines
head -3 sample.log               # First 3 log entries

tail multi_line.txt              # Last 10 lines
tail -n 3 sample.log             # Last 3 log entries
tail -5 numbers.txt              # Last 5 numbers

# Part D: Content Analysis
wc multi_line.txt                # Count lines, words, characters
wc -l *.txt                      # Count lines in all text files
wc -w sample.log                 # Count words in log file

# Part E: Search and Filter
grep "ERROR" sample.log          # Find error entries
grep -n "INFO" sample.log        # Find info entries with line numbers
grep -v "DEBUG" sample.log       # Exclude debug entries
grep -c "INFO" sample.log        # Count info entries

# Part F: File Information
file *.txt                       # Identify file types
ls -lh                           # See file sizes
stat multi_line.txt              # Detailed file information

✅ Expected Results:
□ Comfortable viewing files with cat, less, more
□ Efficient navigation within less viewer
□ Understanding of head/tail for partial viewing
□ Ability to search within files using grep
□ Knowledge of file analysis tools (wc, file, stat)
```

#### **Exercise 4: Wildcard Pattern Mastery**
```bash
# 🎯 Exercise 4: Advanced Pattern Matching
# Master wildcards and pattern matching

# Setup: Create diverse files for pattern practice
cd ~/file_workshop
mkdir wildcard_practice
cd wildcard_practice

# Create test files with various patterns
touch file1.txt file2.txt file3.txt
touch fileA.txt fileB.txt fileC.txt
touch report_2024_01.pdf report_2024_02.pdf report_2023_12.pdf
touch test01.py test02.py test10.py test99.py
touch backup.tar.gz backup.zip backup.bz2
touch config.conf system.conf network.conf
touch image1.jpg image2.png image3.gif
touch log_monday.txt log_tuesday.txt log_friday.txt
touch data_a1.csv data_b2.csv data_c3.csv
touch .hidden1 .hidden2 .config

# Part A: Basic Asterisk Patterns
ls *.txt                         # All text files
ls file*                         # Files starting with 'file'
ls *2024*                        # Files containing '2024'
ls report*                       # Files starting with 'report'
ls *.py                          # All Python files

# Part B: Question Mark Patterns
ls file?.txt                     # Single character after 'file'
ls test??.py                     # Two characters after 'test'
ls image?.???                    # Single char + three-char extension

# Part C: Bracket Patterns
ls file[123].txt                 # Files with 1, 2, or 3
ls file[A-C].txt                 # Files with A, B, or C
ls test[0-9][0-9].py            # Two-digit test files
ls *[0-9].???                   # Files ending with digit + 3-char extension

# Part D: Negation Patterns
ls [!.]*.txt                     # Text files not starting with dot
ls file[!0-9].txt               # file + non-digit + .txt
ls *[!z].py                     # Python files not ending with 'z'

# Part E: Complex Combined Patterns
ls *[0-9]*.[pt]*                # Files with digit and extension starting p or t
ls [tf]*[0-9].???               # Files starting with t/f, containing digit
ls {*.txt,*.py}                 # Multiple extensions (brace expansion)

# Part F: Practical Pattern Applications
# Copy operations with patterns
mkdir sorted
cp *.txt sorted/                 # Copy all text files
cp *2024* sorted/               # Copy all 2024 files
cp test[0-5]*.py sorted/        # Copy test files 0-5

# Move operations with patterns
mkdir archive
mv *backup* archive/            # Move all backup files
mv .*config archive/            # Move hidden config files

# Delete operations with patterns (be careful!)
ls *.tmp                        # Check what would be deleted first
# rm *.tmp                      # Would delete if any existed

# Count and analyze with patterns
echo "Text files: $(ls *.txt | wc -l)"
echo "Python files: $(ls *.py | wc -l)"
echo "2024 files: $(ls *2024* | wc -l)"

✅ Expected Results:
□ Master use of * for any characters
□ Effective use of ? for single characters
□ Proficient with [] for character sets and ranges
□ Understanding of negation with [!]
□ Ability to combine patterns for complex matching
□ Safe application of patterns in file operations
```

---

## 📋 Interview Questions

### **Command-Line Skills Assessment**

#### **Question 1: Navigation and Filesystem**
```
Q: You're currently in /home/user/documents. Write the commands to:
   a) Navigate to the root directory
   b) Go to /var/log directory  
   c) Return to your home directory
   d) Go back to the previous directory (/var/log)

Expected Answer:
a) cd /
b) cd /var/log
c) cd ~ or cd /home/user
d) cd -
```

#### **Question 2: File Operations**
```
Q: What's the difference between these commands?
   - cp file.txt backup.txt
   - mv file.txt backup.txt
   - ln -s file.txt backup.txt

Expected Answer:
- cp: Creates a copy, original file remains
- mv: Moves/renames file, original file is gone
- ln -s: Creates symbolic link, original file remains, link points to it
```

#### **Question 3: Wildcard Patterns**
```
Q: Match these wildcard patterns with their descriptions:
   a) *.txt
   b) file?.log
   c) [0-9][0-9].dat
   d) *[!0-9]*

Expected Answer:
a) All files ending with .txt
b) Files like file1.log, fileA.log (single character after 'file')
c) Two-digit numbered files ending with .dat (00.dat to 99.dat)
d) Files containing at least one non-digit character
```

#### **Question 4: Content Viewing**
```
Q: Which command would you use to:
   a) View the first 20 lines of a large log file
   b) Monitor a log file for new entries in real-time
   c) Count the number of lines in a file
   d) Search for "ERROR" in a log file

Expected Answer:
a) head -n 20 logfile.txt or head -20 logfile.txt
b) tail -f logfile.txt
c) wc -l filename.txt
d) grep "ERROR" logfile.txt
```

#### **Question 5: System Knowledge**
```
Q: Explain what these directories are used for:
   a) /etc
   b) /var/log
   c) /tmp
   d) /home

Expected Answer:
a) /etc - System configuration files
b) /var/log - System and application log files
c) /tmp - Temporary files (cleared on reboot)
d) /home - User home directories
```

---

## 🎯 Summary and Next Steps

### **Day 3 Accomplishments**

✅ **Command-Line Mastery Achieved:**
- Linux filesystem hierarchy understanding
- Navigation commands (cd, pwd, ls, tree)
- File operations (touch, mkdir, mv, cp, rm)
- Content viewing (cat, less, head, tail, grep)
- Wildcards and pattern matching (*, ?, [])
- Essential utilities (clear, history, alias, man)
- Professional efficiency techniques

---

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