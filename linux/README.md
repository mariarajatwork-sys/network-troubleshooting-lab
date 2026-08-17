# Linux Networking Troubleshooting Lab

This lab contains hands-on Linux networking troubleshooting scenarios, commands, and practical exercises.

## Topics

- Network interfaces
- IP configuration
- Routing
- DNS configuration
- Ports and sockets
- Connectivity testing
- Network troubleshooting commands
- Common Linux networking issues

---

## 1. Network Interfaces

### Check Network Interfaces

```bash
ip addr
```

### Check Interface Status

```bash
ip link
```

### Check IP Address in Brief

```bash
ip -br addr
```

### Check a Specific Interface

```bash
ip addr show eth0
```

### Check Interface Statistics

```bash
ip -s link
```
## 2. IP Configuration

### Check IP Address

```bash
ip addr
```

### Add an IP Address

```bash
sudo ip addr add 192.168.1.100/24 dev eth0
```

### Remove IP Address

```bash
sudo ip addr del 192.168.1.100/24 dev eth0
```

### Change IP Address

```bash
sudo ip addr replace 192.168.1.100/24 dev eth0
```



