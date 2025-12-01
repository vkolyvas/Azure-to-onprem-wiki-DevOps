# HAProxy – Installation & Configuration
HAProxy is a TCP/HTTP load balancer and reverse proxy.\
\
**Installation (Ubuntu)**
bash
```
sudo apt update
sudo apt install -y haproxy
```
**Configuration**
1. Edit /etc/haproxy/haproxy.cfg to define:
- Global and defaults sections
- Frontends (listening IP/port, ACLs)
- Backends (server pools, timeouts)
- Health checks and load balancing algorithms
2. Validate configuration and restart:
bash
```
sudo haproxy -c -f /etc/haproxy/haproxy.cfg
sudo systemctl restart haproxy
```

