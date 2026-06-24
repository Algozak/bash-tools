# ProcInspector

A Bash tool that inspects a running process and prints a detailed breakdown — memory, file descriptors, namespaces, cgroup, and binary inode info — pulled directly from `/proc/<PID>/`.

## Features

- PPid
- Process command and state
- Memory usage (VmRSS)
- Open file descriptors count
- Namespaces (PID, NET, MNT)
- Cgroup path
- Threads
- Binary inode and hard link count

## Installation

```bash
git clone https://github.com/Algozak/bash-tools.git
cd bash-tools/ProcInspector
chmod +x procinspector
```

## Usage

```bash
./procinspector <PID>
```

You need the PID of a running process. Find one with `ps aux` or `pgrep <name>`.

### Example

```bash
sleep 1000 &
./procinspector $!
```

### Example output

```
╔══════════════════════════════════╗
║ Process Inspector: PID - 41444   ║
╠══════════════════════════════════╣
║ PPid:        37930               ║
║ State:       S (sleeping)        ║
║ Memory:      2348 kB             ║
║ Open FDs:    12                  ║
║                                  ║
║ Namespaces:                      ║
║ PID:         4026531836          ║
║ NET:         4026531833          ║
║ MNT:         4026531832          ║
║                                  ║
║ Cgroup: 0::/user.slice/user-10...║
║                                  ║
║ Threads:     1                   ║
║                                  ║
║ Binary-inode 285543              ║
║ Binary-links 1:                  ║
╚══════════════════════════════════╝

```

## Notes

- Inspecting processes owned by other users may require `sudo`.

## How it works

All data is read directly from `/proc/<PID>/` — no `lsof`-style external dependencies beyond what's used for file descriptor counting.

