# ProcInspector

A Bash tool that inspects a running process and prints a detailed breakdown — memory, file descriptors, namespaces, cgroup, and binary inode info — pulled directly from `/proc/<PID>/`.

## Features

- Process command and state
- Memory usage (VmRSS)
- Open file descriptors count
- Namespaces (PID, NET, MNT)
- Cgroup path
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
╔════════════════════════════════════╗
║ Process Inspector — PID 47551      ║
╠════════════════════════════════════╣
║ Command: sleep 1000                ║
║ State: S (sleeping)                ║
║ Memory: 2148 kB                    ║
║ Open FDs: 4                        ║
║                                    ║
║ Namespaces:                        ║
║ PID: 4026531836                    ║
║ NET: 4026531840                    ║
║ MNT: 4026531841                    ║
║                                    ║
║ Cgroup: /user.slice/...            ║
║                                    ║
║ Binary inode: 12776                ║
║ Binary links: 1                    ║
╚════════════════════════════════════╝
```

## Notes

- Inspecting processes owned by other users may require `sudo`.

## How it works

All data is read directly from `/proc/<PID>/` — no `lsof`-style external dependencies beyond what's used for file descriptor counting.

