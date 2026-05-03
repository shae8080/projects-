## Phase 2: Host Hardening & Active Defense

### 1. Network Perimeter Security (UFW)
To reduce the attack surface, I implemented a "Default Deny" policy using the Uncomplicated Firewall (UFW). The environment was hardened from 6 open ports down to a single secure entry point.
```bash
# Set default policies
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Allow only essential secure traffic (HTTPS)
sudo ufw allow 443/tcp

# Enable the firewall
sudo ufw enable

# jail.local configuration 
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 3600

# Generate a private key and self-signed certificate
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/apache-selfsigned.key \
-out /etc/ssl/certs/apache-selfsigned.crt

# Securely encrypting sensitive local files
gpg --symmetric --cipher-algo AES256 sensitive_data.txt

# Disable and mask vulnerable services
sudo systemctl stop vsftpd
sudo systemctl disable vsftpd
sudo systemctl mask smbd
