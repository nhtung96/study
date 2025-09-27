# 🚦 Troubleshooting Decision Tree 
## 🐳 Container/Service Issues
- **Service won’t start**
  - `systemctl status <service>` → check status
  - `journalctl -xe -u <service>` → view logs
  - `docker logs <container>` OR `kubectl logs <pod>` → container logs
  - If dependency failure → `systemctl list-dependencies <service>`
  - If config issue → check `/etc/<service>/` configs

- **Container stuck/crashing**
  - `docker ps -a` OR `kubectl get pods` → container state
  - `docker logs <id>` OR `kubectl describe pod <pod>` → failure reason
  - Resource pressure? → `top`, `df -h`, `iostat`
  - Networking? → `curl <service-endpoint>` inside pod
  - Fix → restart container, update config, redeploy with `helm/ansible`

---

## 🌐 Network Issues
- **Can’t reach external host**
  - `ping 8.8.8.8` → basic connectivity
  - `ip route` → check default gateway
  - `ss -tulnp` → verify local service listening
  - `iptables -L -n` / `nft list ruleset` → firewall
  - `traceroute <host>` OR `mtr <host>` → routing path
  - DNS? → `dig <domain>` / `resolvectl query <domain>`

- **Port blocked**
  - `nc -zv host port` → connectivity check
  - `tcpdump -i eth0 port <port>` → see packets
  - Cloud security groups? (OpenStack/K8s/Edge FW rules)

---

## 💾 Storage Issues
- **Disk full**
  - `df -h` → filesystem usage
  - `du -sh /var/*` → find large dirs
  - Logs? → `/var/log/`
  - Containers? → `docker system df` OR prune old images
  - Fix → cleanup, extend volume (`lvextend + resize2fs`)

- **New disk not visible**
  - `lsblk` → see if device detected
  - `dmesg -T | grep sdX` → kernel log for disk
  - `fdisk -l` → confirm partitions
  - If missing → rescan SCSI bus: `echo "- - -" > /sys/class/scsi_host/host0/scan`

---

## 🖥️ Performance Issues
- **High CPU**
  - `top` / `htop` → process using CPU
  - `ps -o pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head`
  - Debug process with `strace -p <pid>`

- **High Memory**
  - `free -m` → memory usage
  - `top` → find high-memory process
  - Container memory leaks? → `docker stats`

- **Disk I/O bottleneck**
  - `iostat -xz 1` → IOPS & wait time
  - `iotop` (if installed) → per-process I/O
  - Fix → balance load, move to faster disk/SSD

---

## ☁️ Cloud/Edge-Specific
- **OpenStack VM not reachable**
  - `openstack server list` → check status
  - `openstack port list` → verify network port
  - Security group rules? → `openstack security group rule list`
  - Hypervisor logs → `/var/log/nova/nova-compute.log`

- **Kubernetes Pod not responding**
  - `kubectl get pods -n <ns>` → pod status
  - `kubectl describe pod <pod>` → events
  - Node pressure? → `kubectl describe node <node>`
  - Network plugin (CNI) → check `kubectl get pods -n kube-system`
  - Restart with `kubectl delete pod`

- **Ceph storage degraded**
  - `ceph -s` → health check
  - `ceph osd tree` → OSD status
  - `journalctl -u ceph-osd@<id>` → logs
  - Recover → `ceph osd reweight <id>`, replace failed disk

---

## ✅ General Incident Response Workflow
1. **Identify**: What is failing? (service, network, storage, VM)  
2. **Check logs**: `journalctl`, `docker logs`, `kubectl logs`  
3. **Check resources**: `df -h`, `top`, `iostat`, `ip addr`  
4. **Narrow down**: Is it config, resource, or external dependency?  
5. **Fix & verify**: Apply change, then `systemctl status` / `kubectl get pods`  
6. **Document**: Add to runbook for next time  

