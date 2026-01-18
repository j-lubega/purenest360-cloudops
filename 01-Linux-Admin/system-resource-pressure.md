# Troubleshooting High System Load
**Scenario:** User reports the Linux server is extremely slow/unresponsive.

### 1. Investigation Steps
* **Check Load Average:** Run `top` or `uptime`. Look at the 1, 5, and 15-minute averages.
* **Identify the Culprit:** Press `Shift + P` in `top` to sort by CPU usage or `Shift + M` for Memory.
* **Check Disk I/O:** Run `iostat -xz 1` or `iotop`. High `%util` means the disk is the bottleneck.

### 2. Common Solutions
* **High CPU:** If a process is runaway, use `kill -15 [PID]` (Graceful) or `kill -9 [PID]` (Forced).
* **High Memory:** Check for OOM (Out of Memory) kills in logs: `dmesg | grep -i oom`.
* **Zombie Processes:** Identify with `ps aux | awk '{ print $8 " " $2 }' | grep -w Z`.
