# Linux Command Cheat Sheet for Infrastructure Engineers (IaaS v2.0 / Edge)

## 🖥️ System Management
- `uname -a` → Kernel & OS info  
- `lsb_release -a` → Distribution details  
- `uptime` → System uptime & load  
- `top`, `htop` → Monitor processes & resources  
- `ps aux | grep <proc>` → Find running processes  
- `systemctl start|stop|restart|status <service>` → Manage services  
- `journalctl -xe` → View logs  
- `dmesg -T` → Kernel messages  

---

## 💾 Storage & Filesystems
- `lsblk` → List block devices  
- `df -h` → Disk usage (human-readable)  
- `du -sh *` → Directory sizes  
- `mount`, `umount` → Mount/unmount storage  
- `fdisk -l`, `parted` → Manage partitions  
- `mkfs.ext4 /dev/sdX` → Format partition  
- **LVM**:  
  - `pvcreate /dev/sdX`  
  - `vgcreate vgname /dev/sdX`  
  - `lvcreate -L 10G -n lvname vgname`  
  - `lvextend -L +5G /dev/vgname/lvname`  
  - `resize2fs /dev/vgname/lvname`  
- `xfs_growfs /mountpoint` → Grow XFS filesystem  

---

## 🌐 Networking
- `ip addr` → Show interfaces  
- `ip link set dev eth0 up|down` → Enable/disable NIC  
- `ip route` → Show routing table  
- `ss -tulnp` → Show listening ports  
- `ping <host>` → Connectivity test  
- `traceroute <host>` → Route path  
- `mtr <host>` → Live traceroute + ping  
- `tcpdump -i eth0 port 80` → Packet capture  
- `curl -v <url>` → Test HTTP(S) endpoints  
- `wget <url>` → Download files  

---

## 🔒 Security & Access
- `chmod 644 file`, `chmod +x script.sh` → File permissions  
- `chown user:group file` → Change ownership  
- `ssh user@host` → Remote access  
- `scp file user@host:/path` → Secure copy  
- `rsync -avz file user@host:/path` → Efficient file transfer  
- `iptables -L -v -n` → Firewall rules (legacy)  
- `nft list ruleset` → Firewall rules (modern)  
- `ufw allow 22/tcp` → Open SSH port  
- `openssl s_client -connect host:443` → Debug TLS/SSL  

---

## 🐳 Containers & Virtualization
- **Docker**:  
  - `docker ps` → Running containers  
  - `docker logs <id>` → Logs  
  - `docker exec -it <id> bash` → Enter container  
- **Podman**:  
  - `podman ps` → Running containers  
- **KVM/Libvirt**:  
  - `virsh list` → VMs  
  - `virsh console <vm>` → Access VM console  
- **QEMU**:  
  - `qemu-img info|create|convert` → Manage VM disk images  

---

## ☁️ Cloud & Edge (IaaS v2.0)
- **OpenStack CLI**:  
  - `openstack server list`  
  - `openstack network list`  
- **Kubernetes (K8s)**:  
  - `kubectl get nodes,pods,svc`  
  - `kubectl logs <pod>`  
  - `kubectl exec -it <pod> -- bash`  
- **Ceph Storage**:  
  - `ceph -s` → Cluster status  
  - `rados df` → Pool usage  
- **Automation**:  
  - `ansible-playbook site.yml`  
  - `helm install <chart>`  

---

## ⚡ Troubleshooting & Diagnostics
- `strace -p <pid>` → Trace syscalls  
- `lsof -i :80` → Show process using port 80  
- `lsof /path/file` → Show process holding file  
- `vmstat 1` → CPU/memory stats  
- `iostat -xz 1` → Disk I/O  
- `sar -n DEV 1` → Network stats  
- `nc -zv host port` → Test TCP port  
- `dig <domain>` → DNS query  
- `resolvectl query <domain>` → Systemd DNS query  

---

✅ **Tip**: Keep this file in GitHub as `linux_infra_commands.md` and update it when you learn new tricks.  
