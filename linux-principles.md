# Linux Core Principles

A quick orientation for newcomers to the Linux operating system.

## 1. The Kernel
The **kernel** is the heart of Linux. It loads first at boot and runs continuously, and it alone talks to the hardware — CPU, memory, disks, network cards. Its main jobs:

- **Process scheduling** — decides which program runs on the CPU and when.
- **Memory management** — allocates RAM, isolates each process's memory, and uses swap when RAM is full.
- **Device drivers** — code inside the kernel that handles specific hardware.
- **System calls (syscalls)** — the official doorways through which programs request kernel services such as reading a file, opening the network, or starting a process.

## 2. User Space vs. Kernel Space
Linux splits the world into two zones to protect the system:

- **Kernel space** — privileged, with full access to hardware. Only the kernel runs here.
- **User space** — where your applications, desktop, shell, and servers live. They cannot touch hardware directly; every request goes through a syscall.

This isolation is why a crashing app usually does not crash the whole machine.

## 3. Everything Is a File
One of Linux's most distinctive ideas: nearly everything — documents, directories, hard drives, keyboards, network sockets, printers — is represented as a **file** in a single tree starting at the root `/`. You read and write them with the same commands (`cat`, `echo`, `ls`). This unifies a huge range of resources under one simple model.

## 4. The Filesystem Hierarchy
Standard directories have fixed roles:

| Directory | Role |
|-----------|------|
| `/bin`, `/usr/bin` | Essential and user programs |
| `/etc` | System configuration files |
| `/home` | Users' personal files (e.g. `/home/patrice`) |
| `/var` | Logs, mail, spools |
| `/tmp` | Temporary files |
| `/dev` | Device files — the "everything is a file" entry points to hardware |
| `/proc`, `/sys` | Live views of the kernel and hardware |

## 5. Users, Groups, and Permissions
Every file and process belongs to an **owner** and a **group**. Each file carries three permission sets — **read (r)**, **write (w)**, **execute (x)** — for the *owner*, the *group*, and *others*:

| Symbol | Owner | Group | Others | Meaning |
|--------|-------|-------|--------|---------|
| `rwxr-xr--` | `rwx` | `r-x` | `r--` | Owner can do anything; group can read and execute; others can only read |

The `chmod` and `chown` commands change these. A special user, **root** (the "superuser"), bypasses all permission checks — use it sparingly, typically via `sudo`.

## 6. Processes
A **process** is a running program. Each gets an ID (**PID**) and its own memory. Key ideas:

- **Parent/child** — every process is started by another; the first is `init` (today usually `systemd`, PID 1).
- **Daemons** — background services that run without a terminal (e.g. `sshd`, `nginx`).
- **Signals** — messages to processes; `Ctrl-C` sends `SIGINT`, `kill` sends `SIGTERM`.

## 7. The Shell and Package Management
- **Shell** (e.g. `bash`): the command interpreter where you type commands and write scripts.
- **Package manager** (e.g. `apt` on Debian/Ubuntu, `dnf` on Fedora): installs, updates, and removes software from trusted repositories — the recommended way to get software on Linux.

## 8. Philosophy
Linux inherits the Unix philosophy: **do one thing well**, combine small tools via pipes (`|`), prefer plain text, and keep configuration in editable files. The result is a system that is powerful, scriptable, and transparent.
