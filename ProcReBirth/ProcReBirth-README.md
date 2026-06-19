ProcReBirth

A minimal process supervisor written in Bash — runs a command, watches it, and automatically restarts it if it dies. A simplified version of what systemd does with restart policies.

Features


Runs any command and tracks its PID
Live spinner shows monitoring status in the terminal
Automatic restart on crash
All events (start/death/restart) logged to a file with timestamps — the terminal stays clean, the log keeps the history


Installation

bashgit clone https://github.com/Algozak/bash-tools.git
cd bash-tools/ProcReBirth
chmod +x procrebirth

Usage

bash./procrebirth "<command>"

The command must be passed as a single quoted string.

Example

bash./procrebirth "sleep 30"

[/] Monitoring...

If the process dies, you'll see:

The process has died

Restarting process!

Logs are saved in monitor.log

Example log output (monitor.log)

[2026-06-19 14:32:01] [INFO] Process Started: sleep 30 (PID 12345)
[2026-06-19 14:32:31] [ERROR] Process Died: sleep 30 (PID 12345)
[2026-06-19 14:32:32] [INFO] Process Started: sleep 30 (PID 12389)

How it works

The monitor checks process liveness using kill -0 "$pid" — a signal that doesn't kill anything, just checks if the process still exists. The spinner loop doubles as the health check: as long as it's spinning, the process is alive; when it exits, the process has died.

Notes


Press Ctrl+C to stop the monitor (this also stops the spinner; the supervised process itself is not separately cleaned up — keep this in mind for long-running use).
The log file (monitor.log) is created in the current working directory.
