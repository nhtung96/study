# Infrastructure Engineer notes

## 1. Linux System Operations
- **systemctl**
  - Start/stop/restart service
  - Enable/disable service at boot
  - `systemctl status <service>`
- **journalctl**
  - `journalctl -u <service>` → service logs
  - `journalctl -b` → logs from current boot
  - Persistent log: `/var/log/journal/`
- **Log files**
  - Syslog: `/var/log/syslog` or `/var/log/messages`
  - Auth log: `/var/log/auth.log`
- **Resource check**
  - `top`, `htop`, `free -h`, `df -h`, `iostat`

---

## 2. Networking Basics 
- **IP / Routing**
  - `ip addr`, `ip route`, `ping`, `traceroute`
- **DNS**
  - `dig <domain>`, `nslookup`, `/etc/resolv.conf`
- **Firewall**
  - `iptables -L`, `nft list ruleset`
- **TCP/UDP Troubleshooting**
  - `ss -tulnp`, `netstat -an`
  - `tcpdump -i eth0 port 80`
- **Network concepts interviewer cares about**
  - VLAN, MTU, bonding/teaming
  - NAT vs SNAT vs DNAT
  - Load balancing basics (L4 vs L7)

---

## 3. Automation & Tools
- **Ansible**
  - Inventory file, ad-hoc commands
  - Example: `ansible all -m ping`
  - Playbook: YAML structure
- **Terraform (basic awareness)**
  - Declarative infra-as-code
  - `terraform init/plan/apply`
- **Bash/Python**
  - Loops, conditions, parsing text (`awk`, `grep`, `jq`)
  - Python: requests, json, subprocess for infra automation

---

## 4. Cloud / OpenStack
- **Core services**
  - Compute: Nova
  - Networking: Neutron
  - Storage: Cinder/Swift
- **Concepts**
  - VM lifecycle, floating IPs, security groups
  - Overlay networking (VXLAN/GRE)
- **Hands-on cmds**
  - `openstack server list`
  - `openstack network list`
  - `openstack volume list`

---

## 5. Containers / Kubernetes (High-level Only)
- **Containers vs VMs**: lightweight, share kernel
- **Basic kubectl**
  - `kubectl get pods`, `kubectl logs <pod>`, `kubectl describe`
- **Concepts to know**
  - Pod, Deployment, Service
  - Control plane vs worker node
- (Don’t go deep — just show awareness)

---

## 6. Troubleshooting Mindset
- **Method**
  1. Define the problem (symptoms, scope)
  2. Check system status (`systemctl`, `journalctl`)
  3. Verify network connectivity (ping, curl, tcpdump)
  4. Check logs (`/var/log/`, `journalctl`, app logs)
  5. Isolate layers (infra vs app vs config)
- **Golden tools**
  - `ping`, `curl`, `dig`, `tcpdump`
  - `journalctl`, `systemctl`, `top`

---

## 7. Communication
- Be clear: state assumptions, troubleshooting steps
- Avoid jargon if not needed
- Show structured thinking (layer by layer)

---
