# SysOver

A minimalistic Bash tool that displays a quick system overview — CPU, memory, uptime, and disk usage — parsed directly from `/proc`.

## Features

- CPU model 
- Memory usage (used / total) 
- System uptime (days/hours/minutes)
- Disk usage (size / used / available)

## Installation

```bash
git clone https://github.com/Algozak/bash-tools.git
cd bash-tools/SysOver
chmod +x sysover 
```

## Usage

```bash
./sysover
```

No flags, no arguments — just run it.

### Example output

```
╔════════════════════════════════════════════════╗
║              System Overview                   ║
╠════════════════════════════════════════════════╣
║ CPU: Intel(R) Core(TM) i3-1005G1 CPU @ 1.20GHz ║
║ Memory: 3.42 GB / 7.56 GB                      ║
║ Uptime: 0d 20h 44m                             ║
║ Disk: size | used | avail                      ║
║       91G    24G    65G                        ║
╚════════════════════════════════════════════════╝
```

## How it works

All data is read directly from kernel pseudo-filesystems (`/proc`) — no external tools like `top` or `free` are used for the core metrics.

