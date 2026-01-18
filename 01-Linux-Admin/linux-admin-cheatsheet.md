
🐧 Linux Administration: The Support Engineer's Linux Cheatsheet

Author: Jimmy Lubega

Focus: System Health, Troubleshooting, and Performance Tuning

1. The Essentials (Navigation & File Operations)
   
Command           | Meaning / Use Case
------------------ | -----------------------------------------------------------------------
pwd                   | Print Working Directory: Shows exactly where you are.
ls -lah               | List Files: Shows all files (including hidden) with sizes in KB/MB/GB.
cd ..                 | Jump Back: Switches back to the previous directory you were in.
mkdir -p a/b/c        | Make Parent: Creates a nested directory structure in one go.
cp -r                 | Recursive Copy: Used to copy entire folders.
mv old_name new_name  | Move/Rename: Used to rename files or move them to new paths.
rm -rf                | Force Delete: Deletes a folder and all its contents (Use with caution).

2. Searching & Filtering (The "Grep" Power)
   
Command                  | Meaning / Use Case
------------------------|--------------------------------------------------------------
grep -i "error" log.txt| Search Text: Finds "error" in a file (ignores case).
grep -r "192.168.1.1" /etc/| Recursive Search: Finds which config file contains a specific IP.
awk '{print $1}' file.txt | Column Filter: Prints only the first column of a text file.
sed -i 's/old/new/g' file | Stream Editor: Replaces "old" with "new" directly inside the file.
find /var/log -mtime -7 | Find Recent: Finds files modified in the last 7 days.
locate filename        | Quick Find: Uses an indexed database to find files instantly.

3. System Health & Performance
   
Command                   | Meaning / Use Case
---------------------------|--------------------------------------------------------------
top                        | Real-time view of CPU and Memory usage.
htop                       | Interactive Top: A more readable, colourised version of top.
uptime                     | Load Average: Shows 1, 5, and 15-minute system load averages.
free -h                    | Memory Check: Shows available, used, and swap memory in GB.
df -h                     | Disk Space: Shows how full your partitions are and their type (ext4, xfs).
du -sh * | sort -h  | Disk Usage: Lists files in current directory sorted by size (finds "space hogs").
iostat -xz 1             | Disk I/O: Shows if the disk is slow (high %util).

4. Users, Permissions & Security
   
Command                   | Meaning / Use Case
--------------------------|--------------------------------------------------------------
chmod 400 key.pem         | Secure Key: Makes a file readable only by the owner (standard for SSH).
chown -R user:group dir    | Change Owner: Changes ownership of a folder and all its contents.
sudo !!                   | Run as Root: Repeats the last command as a superuser.
last                       | Login History: Shows who has logged in recently.
history | grep "ssh" | Command History: Finds that long SSH command you ran yesterday.
id                         | Identity: Shows your current UserID (UID) and GroupID (GID).

5. Networking & Connectivity (TSE Focus)
   
Command                    | Meaning / Use Case
--------------------------|--------------------------------------------------------------
ip addr show                | Check IP: Modern replacement for ifconfig.
ss -tulpn                   | Socket Stats: Shows which apps are listening on which ports.
dig +short google.com | DNS Lookup: Quickly finds the IP address of a domain.
curl -Iv https://site.com | Inspect Headers: Debugs SSL certificates and HTTP response codes.
mtr google.com             | Network Trace: A better traceroute that shows packet loss per hop.
nc -zv 10.0.0.1 80        | Netcat Port Check: Checks if a remote port is open without a full connection.
tcpdump -i eth0           | Packet Sniffer: Capture network traffic for deep analysis.

6. Logs & Advanced Troubleshooting
   
Command                   | Meaning / Use Case
--------------------------|--------------------------------------------------------------
tail -f /var/log/syslog   | Live Logs: Follows the system log as it happens.
journalctl -u nginx -f  | Service Logs: Follows logs for a specific systemd service (e.g., Nginx).
dmesg -T | grep -i oom   | Kernel Errors: Checks if the system killed a process due to "Out of Memory".
lsof -p <PID>               | List Open Files: Shows every file a specific process is touching.
strace -p <PID>            | System Trace: Watches every system call a process makes (the "ultimate" debugger).
fuser -k 80/tcp            | Port Killer: Finds and kills the process blocking port 80.

7. Package & Service Management
   
Command                     | Meaning / Use Cases
----------------------------|--------------------------------------------------------------
systemctl status <svc>     | Service Status: Check if a service is running/failed.
systemctl restart <svc>    | Restart: Applies config changes to a service.
systemctl enable <svc>     | Autostart: Sets service to start automatically on boot.
apt update && apt upgrade | Debian/Ubuntu: Updates the package list and upgrades the system.
yum install -y <pkg>       | RHEL/CentOS: Installs a package automatically without asking "Yes."

