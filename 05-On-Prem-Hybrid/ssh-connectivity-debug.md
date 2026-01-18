# Debugging SSH Failures (Port 22)
**Scenario:** Unable to connect to a remote server via SSH.

### 1. Investigation Steps
* **Verbosity:** Run `ssh -vvv user@ip` to see exactly where the handshake fails.
* **Port Check:** Run `nc -zv [ip] 22` to see if the port is even open.
* **Trace:** Run `mtr [ip]` to see if packets are dropping at a specific network hop.

### 2. Common Solutions
* **Firewalls:** Ensure `ufw` or `iptables` allows port 22.
* **Key Permissions:** Ensure your private key is protected: `chmod 400 ~/.ssh/id_rsa`.
