## Phase 2: Host Hardening & Active Defense

### 1. Network Perimeter (UFW)
Implemented a "Default Deny" policy. The attack surface was reduced from 6 open ports to 1 secure port[cite: 1].
```bash
sudo ufw default deny incoming
sudo ufw allow 443/tcp
