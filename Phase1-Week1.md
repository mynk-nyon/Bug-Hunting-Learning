# Week 1 — Linux & WSL Mastery

> Cyber-Security-Teacher track · Lessons 1–4 · Ubuntu 26.04 LTS on WSL2
> Quiz answers are hidden under "Reveal answer" — click to expand (works natively on GitHub).

## Table of Contents
- [Lesson 1 — Linux Fundamentals & Why It Matters](#lesson-1--linux-fundamentals--why-it-matters)
- [Lesson 2 — Terminal Navigation & Filesystem Hierarchy](#lesson-2--terminal-navigation--filesystem-hierarchy)
- [Lesson 3 — File Operations & Viewing](#lesson-3--file-operations--viewing)
- [Lesson 4 — Permissions & Ownership](#lesson-4--permissions--ownership)
- [Practice Log](#practice-log)

---

## Lesson 1 — Linux Fundamentals & Why It Matters

### Theory
Almost the entire internet — servers, cloud infrastructure, routers, IoT devices, and nearly every security tool (nmap, Burp, sqlmap, Metasploit) — runs on Linux. Even when the *target* is Windows, the *attacking machine* is almost always Linux. Knowing Linux isn't optional for a security career; it's the native language of the field.

| Concept | Meaning |
|---|---|
| **Linux** | Free, open-source OS kernel; many "distributions" (distros) package it differently |
| **Distro families** | Debian/Ubuntu (beginner-friendly, huge community), Red Hat/Fedora (enterprise), Arch (advanced) |
| **WSL** | Windows Subsystem for Linux — a real Linux environment running inside Windows 11, no VM/dual-boot needed |

**Analogy:** Cybersecurity is detective work; Linux is the toolkit and the language most crime scenes (servers) are written in.

### Quiz — Lesson 1

**Q1. Why do security professionals need Linux skills even when attacking a Windows target?**
<details><summary>Reveal answer</summary>
Because almost every attacking tool and the attacker's own machine typically run on Linux, even if the target OS is Windows.
</details>

**Q2. What is WSL?**
<details><summary>Reveal answer</summary>
Windows Subsystem for Linux — lets you run a genuine Linux kernel/userspace directly inside Windows 11, without a VM or dual-boot.
</details>

**Q3. What distro family is Ubuntu part of?**
<details><summary>Reveal answer</summary>
Debian family (Ubuntu is built on Debian).
</details>

**Q4. True or False: A "distro" and the "Linux kernel" are the same thing.**
<details><summary>Reveal answer</summary>
False. The kernel is the core; a distro packages the kernel together with tools, package managers, and defaults (e.g. Ubuntu, Fedora, Arch all share a kernel lineage but differ heavily in packaging).
</details>

**Q5. Name two command-line security tools that run natively on Linux.**
<details><summary>Reveal answer</summary>
Any two of: nmap, Burp Suite, sqlmap, Metasploit, hydra, John the Ripper, etc.
</details>

**Q6. Which command shows your current Linux distro and version details?**
<details><summary>Reveal answer</summary>
`lsb_release -a` or `cat /etc/os-release`
</details>

### Learn more
- [Linux Journey](https://linuxjourney.com/) — free guided Linux fundamentals
- [Microsoft WSL official docs](https://learn.microsoft.com/en-us/windows/wsl/)
- [DistroWatch](https://distrowatch.com/) — compare distro families

---

## Lesson 2 — Terminal Navigation & Filesystem Hierarchy

### Theory
Linux has **one single tree** starting at `/` (root) — unlike Windows' separate `C:\`, `D:\` drives. Everything, including WSL's view of your Windows drives, hangs off that one tree.

**Analogy:** `/` is the top floor of a building; every folder is a room reached by going down hallways. You're always standing in exactly one room (`pwd` tells you which).

| Path | What's there |
|---|---|
| `/` | Root of everything |
| `/home/<you>` | Your personal files (shortcut `~`) |
| `/etc` | System config files |
| `/var` | Logs, variable data |
| `/tmp` | Temp files, wiped on reboot |
| `/bin`, `/usr/bin` | Executable programs |
| `/mnt/c` | WSL-specific: your Windows C: drive |

| Command | Purpose |
|---|---|
| `pwd` | Print working directory |
| `ls` / `ls -la` | List files (`-l` detail, `-a` hidden files) |
| `cd <path>` | Change directory (`cd ..` up, `cd ~` home, `cd -` previous) |

### Quiz — Lesson 2

**Q1. What does `pwd` stand for and do?**
<details><summary>Reveal answer</summary>
"Print working directory" — shows the full path of the directory you're currently in.
</details>

**Q2. What's the difference between `ls -l` and `ls -a`?**
<details><summary>Reveal answer</summary>
`-l` = long/detailed format (permissions, owner, size, date). `-a` = show hidden files (names starting with `.`). They can be combined as `-la`.
</details>

**Q3. Where does WSL mount your Windows C: drive?**
<details><summary>Reveal answer</summary>
`/mnt/c`
</details>

**Q4. What does `cd ..` do versus `cd ~`?**
<details><summary>Reveal answer</summary>
`cd ..` moves up one directory level. `cd ~` jumps straight to your home directory regardless of where you are.
</details>

**Q5. What makes a file or folder "hidden" in Linux?**
<details><summary>Reveal answer</summary>
Its name starts with a dot (`.`), e.g. `.bashrc`. `ls` hides these by default; `ls -a` reveals them.
</details>

**Q6. What does `cd -` do?**
<details><summary>Reveal answer</summary>
Jumps back to the previous directory you were in before your last `cd`.
</details>

**Q7. Where would you look for system-wide configuration files like the user list?**
<details><summary>Reveal answer</summary>
`/etc` (e.g. `/etc/passwd` holds the user list).
</details>

### Learn more
- [Linux Filesystem Hierarchy Standard (explained)](https://www.pathname.com/fhs/)
- [explainshell.com](https://explainshell.com/) — paste any command to see what each part does
- [Linux Journey — Navigation](https://linuxjourney.com/lesson/navigation-move-around-file-system)

---

## Lesson 3 — File Operations & Viewing

### Theory
Creating, copying, moving, deleting files, and reading their contents — all from the keyboard.

| Command | Purpose | Example |
|---|---|---|
| `touch` | Create empty file / update timestamp | `touch notes.txt` |
| `mkdir` / `mkdir -p` | Make directory / nested directories | `mkdir -p labs/week1/day1` |
| `cp` / `cp -r` | Copy file / copy directory recursively | `cp -r labs labs_backup` |
| `mv` | Move **or** rename | `mv notes.txt renamed.txt` |
| `rm` / `rm -r` | Delete file / delete directory + contents | `rm -r labs_backup` |
| `cat` | Dump whole file to screen | `cat notes.txt` |
| `less` | Page through a file (`q` to quit) | `less notes.txt` |
| `nano` | Terminal text editor (Ctrl+O save, Ctrl+X exit) | `nano notes.txt` |

> ⚠️ **`rm` has no recycle bin.** Deletion is instant and permanent — always double-check the path before pressing Enter.

**Analogy:** `cp` = photocopying, `mv` = relocating/renaming the original, `rm` = the shredder (no undo).

### Quiz — Lesson 3

**Q1. What's the key difference between `cp` and `mv`?**
<details><summary>Reveal answer</summary>
`cp` duplicates a file — the original stays. `mv` relocates or renames — the original is gone from its old location.
</details>

**Q2. Why is `rm` riskier than deleting a file in Windows Explorer?**
<details><summary>Reveal answer</summary>
There's no recycle bin/undo — `rm` deletes permanently and immediately.
</details>

**Q3. You need to read a 10,000-line log file. Why use `less` instead of `cat`?**
<details><summary>Reveal answer</summary>
`cat` dumps the entire file at once (floods your terminal); `less` lets you scroll page by page, search, and quit cleanly with `q`.
</details>

**Q4. How do you create nested directories in one command, e.g. `labs/week1/day1`?**
<details><summary>Reveal answer</summary>
`mkdir -p labs/week1/day1` — the `-p` flag creates all missing parent directories.
</details>

**Q5. How do you copy an entire directory, not just one file?**
<details><summary>Reveal answer</summary>
`cp -r sourcefolder destfolder` — the `-r` (recursive) flag is required for directories.
</details>

**Q6. In `nano`, how do you save and then exit?**
<details><summary>Reveal answer</summary>
Ctrl+O (write out / save), press Enter to confirm filename, then Ctrl+X to exit.
</details>

**Q7. What does `echo "text" > file.txt` do, versus `echo "text" >> file.txt`?**
<details><summary>Reveal answer</summary>
`>` overwrites the file with "text" (destroying prior content). `>>` appends "text" to the end of the file, preserving what's already there.
</details>

### Learn more
- [SS64 Linux command reference](https://ss64.com/bash/)
- [Nano editor cheat sheet](https://www.nano-editor.org/dist/latest/cheatsheet.html)
- [Linux Journey — Manipulating Files](https://linuxjourney.com/lesson/manipulating-files-move-copy-remove)

---

## Lesson 4 — Permissions & Ownership

### Theory
Every file/folder has an **owner**, a **group**, and **permissions** for Read / Write / Execute. Misconfigured permissions (world-writable files, risky SUID binaries, over-permissive cloud storage) are classic real-world vulnerabilities.

**Analogy:** A file is a locked room with three keys — one for the owner, one for the group, one for everyone else. Each key can open the door (read), rearrange furniture (write), or let you use what's inside (execute).

**Reading `ls -l`:**
```
-rwxr-xr-- 1 kali kali 220 Oct 7 10:00 script.sh
```
| Part | Meaning |
|---|---|
| `-` (1st char) | File type: `-` file, `d` directory, `l` symlink |
| `rwx` | Owner permissions |
| `r-x` | Group permissions |
| `r--` | Others' permissions |
| `kali kali` | Owner, then group |

**chmod:**
| Numeric | Symbolic | Meaning |
|---|---|---|
| `chmod 755 file` | `chmod u=rwx,g=rx,o=rx file` | Owner full; others read+execute |
| `chmod 644 file` | `chmod u=rw,g=r,o=r file` | Owner read/write; others read only |
| `chmod +x file` | — | Add execute permission |

Numeric values: `r=4, w=2, x=1`, summed per group. `7=rwx`, `5=r-x`, `4=r--`, `6=rw-`.

**chown:**
```bash
chown newowner file
chown newowner:newgroup file
```

### Quiz — Lesson 4

**Q1. In `-rwxr-xr--`, what can "others" (the last three characters) do to this file?**
<details><summary>Reveal answer</summary>
Only read (`r--`) — no write, no execute.
</details>

**Q2. What numeric chmod value gives the owner full access and everyone else nothing?**
<details><summary>Reveal answer</summary>
`chmod 700 file` (owner = 7/rwx, group = 0, others = 0).
</details>

**Q3. What does `chmod +x script.sh` do?**
<details><summary>Reveal answer</summary>
Adds execute permission to the file (commonly needed to run a script directly, e.g. `./script.sh`).
</details>

**Q4. What's the difference between `chmod` and `chown`?**
<details><summary>Reveal answer</summary>
`chmod` changes **permissions** (read/write/execute). `chown` changes **ownership** (which user/group owns the file).
</details>

**Q5. Why are misconfigured permissions a real-world security issue?**
<details><summary>Reveal answer</summary>
World-writable or world-readable sensitive files (configs, keys, SUID binaries) let unauthorized users read secrets or escalate privileges — a very common finding in both CTFs and real bug bounty reports.
</details>

**Q6. Convert `rwxr-xr-x` to its numeric chmod equivalent.**
<details><summary>Reveal answer</summary>
`755` (owner rwx=7, group r-x=5, others r-x=5).
</details>

**Q7. What command changes both the owner and group of `file.txt` to `alice` and `devs`?**
<details><summary>Reveal answer</summary>
`chown alice:devs file.txt`
</details>

**Q8. Why is Bandit a good place to practice permissions concepts?**
<details><summary>Reveal answer</summary>
Each level hides a password behind realistic permission/ownership puzzles (readable-only-by-owner files, SUID binaries, etc.), forcing you to apply `ls -l`, `chmod` logic, and ownership reasoning to progress — not just memorize the theory.
</details>

### Learn more
- [chmod calculator](https://chmod-calculator.com/)
- [Linux Journey — Permissions](https://linuxjourney.com/lesson/file-permissions-read-write-execute)
- [OverTheWire Bandit Wargame](https://overthewire.org/wargames/bandit/) — hands-on permission puzzles

---

## Practice Log

| Date | Lesson | Status | Bandit Level Reached | Notes |
|---|---|---|---|---|
|  | 1 — Linux Fundamentals | ✅ Done |  |  |
|  | 2 — Navigation & Filesystem | ✅ Done |  |  |
|  | 3 — File Operations | ✅ Done |  |  |
|  | 4 — Permissions & Ownership | ✅ Done | *(in progress)* |  |

> Update this table as you clear more Bandit levels. Next up: Lesson 5 — Text Processing & Pipes.
