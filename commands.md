# Linux Commands Reference Guide

This guide is aimed at beginners and intermediate users working on Ubuntu/Debian-style Linux systems. It collects the commands most useful for checking the system, navigating the filesystem, managing services, working with Git, and accessing remote machines. The examples below use `$HOME` and placeholders so they can be adapted to your own setup.

> Safety note: commands such as `sudo`, `apt`, `rm`, `mv`, and `systemctl` can change your system or delete data. Double-check the target path and command before you run it.

---

## Table of Contents
- [Quick Start & Safety](#quick-start--safety)
- [System Status & Information](#system-status--information)
- [File System Navigation](#file-system-navigation)
- [File Operations](#file-operations)
- [Package Management](#package-management)
- [Networking](#networking)
- [SSH & Remote Access](#ssh--remote-access)
- [Systemd & Service Management](#systemd--service-management)
- [Git Version Control](#git-version-control)
- [User & Environment](#user--environment)
- [Database & SQLite](#database--sqlite)
- [Helpful Tips](#helpful-tips)

---

## Quick Start & Safety

### `sudo`
**What it does:** Runs a command with elevated privileges.

**When to use:** Use when installing software, editing protected files, or changing system settings.

**Example:**
```bash
sudo apt update
```

### `rm -rf`
**What it does:** Removes files or directories recursively and forcefully.

**When to use:** Only use when you are certain you want to delete something permanently.

**Example:**
```bash
rm -rf ~/old-project
```

### `which`
**What it does:** Shows whether a command exists on your system and where it is located.

**Example:**
```bash
which sqlite3
```

### `man [command]`
**What it does:** Opens the manual page for a command.

**When to use:** Use when you want details about a command's options and behavior.

**Example:**
```bash
man ls
```

---

## System Status & Information

### `whoami`
**What it does:** Displays the current logged-in username.

**Example:**
```bash
whoami
```

### `pwd`
**What it does:** Prints the absolute path of your current working directory.

**Example:**
```bash
pwd
```

### `echo $HOME`
**What it does:** Displays the current user's home directory.

**Example:**
```bash
echo "$HOME"
```

### `uname -a`
**What it does:** Prints kernel and system information.

**Example:**
```bash
uname -a
```

### `df -h`
**What it does:** Shows disk space usage in a human-readable format.

**Example:**
```bash
df -h
```

### `free -h`
**What it does:** Displays memory usage information in a human-readable format.

**Example:**
```bash
free -h
```

---

## File System Navigation

### `cd`
**What it does:** Changes the current directory.

**Examples:**
```bash
# Go to your home directory
cd ~

# Go to the parent directory
cd ..

# Go to the previous directory
cd -

# Go to a specific directory
cd /path/to/project
```

### `ls -la`
**What it does:** Lists files and directories, including hidden ones, with detailed information.

**Key flags:**
- `-l` - Long format
- `-a` - Show hidden files

**Example:**
```bash
ls -la ~
```

### `find`
**What it does:** Searches for files and directories in a directory hierarchy.

**Examples:**
```bash
# Find files under a folder
find ~/.cahier -maxdepth 3

# Find regular files and print timestamps
find ~/.cahier ~/cahier_logs -type f -printf "%TY-%Tm-%Td %TH:%TM %p\\n" | sort
```

### `mkdir`
**What it does:** Creates a new directory.

**Example:**
```bash
mkdir -p ~/notes/linux
```

### `cp`
**What it does:** Copies files or directories.

**Example:**
```bash
cp file.txt ~/backups/
```

### `cat`
**What it does:** Prints the contents of a file.

**Example:**
```bash
cat file.txt
```

### `tail`
**What it does:** Shows the end of a file, often used for logs.

**Example:**
```bash
tail -n 20 /var/log/syslog
```

### `grep`
**What it does:** Searches text for a pattern.

**Example:**
```bash
grep "error" /var/log/syslog
```

---

## File Operations

### `mv`
**What it does:** Moves or renames files and directories.

**Examples:**
```bash
# Move a file into a directory
mv file.txt ~/projects/

# Rename a file
mv old-name.txt new-name.txt
```

### `rm`
**What it does:** Removes files or directories.

**Warning:** Use this carefully; it can permanently delete data.

**Example:**
```bash
rm file.txt
```

### `file`
**What it does:** Identifies the type of file.

**Example:**
```bash
file ~/cahier_logs/cahier.db
```

---

## Package Management

### `sudo apt update`
**What it does:** Refreshes the package index from configured repositories.

**When to use:** Run this before installing or upgrading software.

**Example:**
```bash
sudo apt update
```

### `sudo apt install [package-name]`
**What it does:** Installs a package and its dependencies.

**Examples:**
```bash
sudo apt install openssh-server
sudo apt install sqlite3
sudo apt install sqlitebrowser
```

### `sudo apt autoremove`
**What it does:** Removes packages that were automatically installed and are no longer needed.

**Example:**
```bash
sudo apt autoremove
```

---

## Networking

### `ip addr show`
**What it does:** Displays network interfaces and IP addresses.

**Example:**
```bash
ip addr show | grep "inet" | grep -v 127.0.0.1
```

**Useful variation:**
```bash
# Show only IPv4 addresses
ip addr show | grep "inet " | grep -v 127.0.0.1
```

### `sudo ufw status`
**What it does:** Shows the current status of the Uncomplicated Firewall (UFW).

**Example:**
```bash
sudo ufw status
```

### `sudo ufw allow [port]/[protocol]`
**What it does:** Adds a firewall rule to allow traffic on a specific port.

**Examples:**
```bash
sudo ufw allow 22/tcp
sudo ufw allow ssh
```

---

## SSH & Remote Access

### `ssh`
**What it does:** Connects to a remote machine securely over SSH.

**Examples:**
```bash
ssh user@192.168.1.100
ssh -p 2222 user@192.168.1.100
ssh user@192.168.1.100 'ls -la'
```

### `systemctl status ssh`
**What it does:** Checks whether the SSH service is running.

**Example:**
```bash
systemctl status ssh
```

---

## Systemd & Service Management

### `systemctl status [service]`
**What it does:** Shows the status of a systemd service, including recent logs.

**Example:**
```bash
systemctl status ssh
```

### `systemctl enable --now [service]`
**What it does:** Enables a service to start at boot and starts it immediately.

**Example:**
```bash
sudo systemctl enable --now ssh
```

### `systemctl start/stop/restart [service]`
**What it does:** Manually starts, stops, or restarts a service.

**Examples:**
```bash
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
```

---

## Git Version Control

### `git config`
**What it does:** Sets Git configuration values.

**Examples:**
```bash
git config --global user.name "your-name"
git config --global user.email "you@example.com"
git config --global --list
```

### `git status`
**What it does:** Shows the current state of the repository.

**Example:**
```bash
git status
```

### `git add [file]`
**What it does:** Stages changes for commit.

**Examples:**
```bash
git add commands.md
git add .
```

### `git commit -m "[message]"`
**What it does:** Creates a commit with the staged changes.

**Example:**
```bash
git commit -m "add linux command notes"
```

### `git push`
**What it does:** Uploads local commits to a remote repository.

**Example:**
```bash
git push
```

### `git remote -v`
**What it does:** Lists the configured remote repositories.

**Example:**
```bash
git remote -v
```

### `git branch -a`
**What it does:** Lists local and remote branches.

**Example:**
```bash
git branch -a
```

### `git log --oneline --max-count=[n]`
**What it does:** Shows recent commits in a compact format.

**Example:**
```bash
git log --oneline --max-count=5
```

---

## User & Environment

### `echo` (with environment variables)
**What it does:** Prints text or the value of environment variables.

**Examples:**
```bash
echo "$HOME"
echo "$USER"
echo "$PATH"
echo "Hello, World!"
```

### Common environment variables
- `$HOME` - User home directory
- `$USER` - Current username
- `$PATH` - Search path for executables
- `$SHELL` - Current shell

---

## Database & SQLite

### `sqlite3`
**What it does:** Opens or creates a SQLite database and runs SQL commands.

**Examples:**
```bash
sqlite3 ~/cahier_logs/cahier.db ".tables"
sqlite3 ~/cahier_logs/cahier.db ".schema entries"
sqlite3 -header -column ~/cahier_logs/cahier.db "SELECT * FROM entries LIMIT 5;"
```

### `.schema`
**What it does:** Shows the `CREATE TABLE` statements for a table.

**Example:**
```bash
sqlite3 ~/cahier_logs/cahier.db ".schema entries"
```

---

## Helpful Tips

### Piping and filtering
**What they do:** Combine commands to transform or filter output.

**Example:**
```bash
ip addr show | grep "inet" | grep -v 127.0.0.1
```

**Key concepts:**
- `|` - Sends output from one command into another
- `grep` - Filters lines matching a pattern
- `grep -v` - Filters lines that do not match

### Common beginner issues

**Command not found:**
```bash
which sqlite3
sudo apt install sqlite3
```

**Permission denied:**
```bash
sudo apt install openssh-server
ls -la ~/.ssh
```

**Repository issues:**
```bash
git remote -v
git remote set-url origin https://github.com/user/repo.git
```

### Keyboard shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+C` | Cancel the current command |
| `Ctrl+Z` | Suspend the current process |
| `Ctrl+D` | Exit the current shell |
| `Tab` | Auto-complete commands and paths |
| `↑/↓` | Navigate command history |
| `Ctrl+L` | Clear the screen |

---

## Quick Reference Card

| Command | Purpose | Example |
|---------|---------|---------|
| `pwd` | Current directory | `pwd` |
| `cd` | Change directory | `cd ~/projects` |
| `ls -la` | List files | `ls -la ~` |
| `whoami` | Current user | `whoami` |
| `sudo` | Run as root | `sudo apt update` |
| `apt install` | Install package | `sudo apt install sqlite3` |
| `systemctl status` | Service status | `systemctl status ssh` |
| `ip addr show` | IP addresses | `ip addr show` |
| `git status` | Git status | `git status` |
| `git add` | Stage changes | `git add file.md` |
| `git commit` | Commit changes | `git commit -m "message"` |
| `git push` | Push commits | `git push` |

---

*This guide was compiled from practical Linux command-line work and is intended as a learning reference.*
