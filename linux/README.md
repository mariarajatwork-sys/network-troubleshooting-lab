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

---

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

---

## 3. Routing

### Check Routing Table

```bash
ip route
```

### Check Default Gateway

```bash
ip route show default
```

### Add a Route

```bash
 sudo ip route add 192.168.2.0/24 via 192.168.1.1
```

### Delete a Route

```bash
sudo ip route del 192.168.2.0/24
```

---

## 4. DNS Configuration

### Check DNS Configuration

```bash
cat /etc/resolv.conf
```

### Test DNS Resolution

```bash
nslookup google.com
```

### Test DNS with dig

```bash
dig google.com
```

### Check DNS Resolution with getent

```bash
getent hosts google.com
```

---

## 5. Ports and Sockets

### Check Listening Ports

```bash
ss -tuln
```

### Check Listening TCP Ports

```bash
ss -ltn
```

### Check Listening UDP Ports

```bash
ss -lun
```

### Check a Specific Port

```bash
ss -ltnp | grep :80
```

### Check Connections

```bash
ss -tun
```

---

## 6. Connectivity Testing

### Test Connectivity with Ping

```bash
ping -c 4 8.8.8.8
```

### Test Connectivity to a Hostname

```bash
ping -c 4 google.com
```

### Test a Specific Port with nc

```bash
nc -zv google.com 443
```

### Test HTTP Connectivity with curl

```bash
curl -I https://google.com
```

---

## 7. Network Troubleshooting Commands

### Trace Network Path

```bash
traceroute google.com
```

### Check DNS and Network Path

```bash
tracepath google.com
```

### Check Hostname

```bash
hostname
```

### Check Hostname Resolution

```bash
hostname -I
```

### Check ARP / Neighbor Table

```bash
ip neigh show
```

### Check Network Interface Errors

```bash
ip -s link
```

---

## 8. Common Network Troubleshooting Scenarios

### Scenario 1: No Network Connectivity

#### Step 1: Check Interface Status

```bash
ip link
```

#### Step 2: Check IP Address

```bash
ip addr
```

#### Step 3: Check Default Gateway

```bash
ip route
```

#### Step 4: Test Gateway Connectivity

```bash
ping -c 4 192.168.1.1
```

#### Step 5: Test Internet Connectivity

```bash
ping -c 4 8.8.8.8
```

#### Step 6: Test DNS Resolution

```bash
nslookup google.com
```

---

### Scenario 2: DNS Resolution Failure

#### Step 1: Check DNS configuration

```bash
 cat /etc/resolv.conf
```

#### Step 2: Test DNS

```bash
nslookup google.com
```

#### Step 3: Test with dig

```bash
dig google.com
```

#### Step 4: Test connectivity using the IP address

```bash
ping -c 4 8.8.8.8
```
#### If IP connectivity works but hostname resolution fails, investigate the DNS configuration.

---

### Scenario 3: Service Port Not Reachable

#### Check whether the service is listening:

```bash
ss -ltnp
```

#### Check a specific port:

```bash
ss -ltnp | grep :80
```

#### Test the remote port:

```bash
nc -zv <server-ip> 80
```

#### Check HTTP connectivity:

```bash
curl -I http://<server-ip>
```

---

### Scenario 4: Network Interface Errors

#### Check interface statistics:

```bash
ip -s link
```
#### Look for:

- RX errors
- TX errors
- Dropped packets
- Collisions
- Packet loss

---

### Scenario 5: Check Network Path

#### Trace the network path:

```bash
traceroute google.com
```

#### Check DNS and network path:

```bash
tracepath google.com
```

#### Check hostname:

```bash
hostname
```

#### Check hostname resolution:

```bash
hostname -I
```

#### Check ARP / Neighbor Table:

```bash
ip neigh show
```

#### Check network interface errors:

```bash
ip -s link
```

#### What to look for:

- RX errors
- TX errors
- Dropped packets
- Collisions
- Packet loss

---

## 9. Common Troubleshooting Workflow

### Step 1: Check Network Interface

```bash
ip addr
ip link
```

### Step 2: Check IP Address

```bash
ip addr show
```

### Step 3: Check Routing

```bash
ip route
ip route show default
```

### Step 4: Check DNS

```bash
cat /etc/resolv.conf
nslookup google.com
dig google.com
```

### Step 5: Test Connectivity

```bash
ping -c 4 8.8.8.8
ping -c 4 google.com
```

### Step 6: Check Listening Ports

```bash
ss -ltn
ss -tun
```

### Step 7: Test HTTP Connectivity

```bash
curl -I https://google.com
```

### Step 8: Trace Network Path

```bash
traceroute google.com
```

### Step 9: Check Network Interface Errors

```bash
ip -s link
```

### Step 10: Check ARP / Neighbor Table

```bash
ip neigh show
```

### Step 11: Check Firewall

```bash
sudo ufw status
sudo iptables -L -n
```

### Step 12: Check Service Status

```bash
systemctl status <service-name>
```

### Step 13: Check Service Logs

```bash
journalctl -u <service-name> --since "10 minutes ago"
```

### Step 14: Check Port Connectivity

```bash
nc -zv <server-ip> <port>
```

### Step 15: Capture Network Traffic

```bash
sudo tcpdump -i any host <server-ip>
```

### Step 16: Verify the Fix

```bash
ping -c 4 <server-ip>
curl -I http://<server-ip>
```

### Step 17: Document the Issue

#### Record:

- Problem observed
- Commands used for troubleshooting
- Root cause
- Fix applied
- Verification result

---

## 10. Network Monitoring and Diagnostic Tools

Network monitoring and diagnostic tools help identify connectivity problems, performance issues, packet loss, latency, open ports, and network traffic.

### 10.1 Check Network Interfaces

Use `ip` to view network interfaces and their configuration.

```bash
ip addr
ip link
```

Useful for checking:

- Interface name
- Interface state
- IP address
- MAC address
- Network configuration

---

### 10.2 Check Routing Table

Use `ip route` to view the routing table.

```bash
ip route
```

Check for:

- Default gateway
- Destination networks
- Network interfaces
- Incorrect routes

To check the default route:

```bash
ip route show default
```

---

### 10.3 Test Connectivity with Ping

`ping` is used to test basic network connectivity.

```bash
ping -c 4 8.8.8.8
```

Test hostname connectivity:

```bash
ping -c 4 google.com
```

Check for:

- Packet loss
- Response time
- Network reachability

---

### 10.4 Check DNS with nslookup

`nslookup` is used to troubleshoot DNS resolution.

```bash
nslookup google.com
```

Check for:

- DNS server being used
- Resolved IP address
- DNS response
- DNS failures

---

### 10.5 Check DNS with dig

`dig` provides detailed DNS query information.

```bash
dig google.com
```

Query a specific DNS server:

```bash
dig @8.8.8.8 google.com
```

Useful for checking:

- DNS response
- Query time
- DNS server
- A records
- CNAME records
- TTL

---

### 10.6 Trace the Network Path

Use `traceroute` to identify the path packets take to a destination.

```bash
traceroute google.com
```

If `traceroute` is unavailable:

```bash
tracepath google.com
```

Useful for identifying:

- Routing path
- Network hops
- Latency
- Packet loss
- Unreachable destinations

---

### 10.7 Check Listening Ports with ss

Use `ss` to view listening and active network connections.

```bash
ss -ltn
```

View TCP and UDP connections:

```bash
ss -tun
```

View processes associated with connections:

```bash
sudo ss -tulpn
```

Useful for checking:

- Listening ports
- Active connections
- TCP connections
- UDP connections
- Applications using ports

---

### 10.8 Test Port Connectivity with netcat

`nc` can be used to test whether a remote port is reachable.

```bash
nc -zv <server-ip> <port>
```

Example:

```bash
nc -zv 192.168.1.10 443
```

Possible results:

```text
Connection succeeded
```

or:

```text
Connection refused
```

or:

```text
Connection timed out
```

---

### 10.9 Test HTTP Connectivity with curl

Use `curl` to test HTTP/HTTPS connectivity.

```bash
curl -I https://google.com
```

Useful for checking:

- HTTP status code
- Server response
- Connection failures
- TLS/SSL issues
- Redirects

To view detailed connection information:

```bash
curl -v https://google.com
```

---

### 10.10 Check ARP / Neighbor Information

Use `ip neigh` to view the neighbor table.

```bash
ip neigh show
```

Useful for checking:

- IP-to-MAC mappings
- Reachable neighbors
- Failed neighbor entries
- Local network connectivity

---

### 10.11 Check Network Interface Statistics

Use `ip -s link` to check interface statistics.

```bash
ip -s link
```

Look for:

- RX packets
- TX packets
- RX errors
- TX errors
- Dropped packets
- Overruns
- Carrier errors

---

### 10.12 Capture Network Traffic with tcpdump

`tcpdump` captures and analyzes network packets.

Capture traffic on all interfaces:

```bash
sudo tcpdump -i any
```

Capture traffic on a specific interface:

```bash
sudo tcpdump -i eth0
```

Capture traffic from a specific host:

```bash
sudo tcpdump -i any host <server-ip>
```

Capture traffic on a specific port:

```bash
sudo tcpdump -i any port 443
```

Useful for identifying:

- Packet flow
- TCP connections
- Retransmissions
- DNS traffic
- ICMP traffic
- Connection attempts

---

### 10.13 Check Firewall Rules

For systems using UFW:

```bash
sudo ufw status
```

For iptables:

```bash
sudo iptables -L -n
```

For nftables:

```bash
sudo nft list ruleset
```

Check for:

- Blocked ports
- DROP rules
- REJECT rules
- Incorrect firewall rules

---

### 10.14 Check Network Services

Check the status of a network-related service.

```bash
systemctl status <service-name>
```

Example:

```bash
systemctl status ssh
```

Restart a service if required:

```bash
sudo systemctl restart <service-name>
```

Check whether a service starts automatically:

```bash
systemctl is-enabled <service-name>
```

---

### 10.15 Check Service Logs

Use `journalctl` to inspect service logs.

```bash
journalctl -u <service-name>
```

Check recent logs:

```bash
journalctl -u <service-name> --since "10 minutes ago"
```

Useful for identifying:

- Service failures
- Configuration errors
- Connection errors
- Authentication problems
- Restart loops

---

### 10.16 Monitor Network Statistics

Use `sar` to monitor network statistics when the `sysstat` package is installed.

```bash
sar -n DEV 1 5
```

Useful for monitoring:

- Network throughput
- Packets received
- Packets transmitted
- Errors
- Interface activity

---

### 10.17 Monitor Network Connections

Use `ss` to monitor active connections.

```bash
ss -s
```

This provides a summary of:

- TCP connections
- UDP connections
- Listening sockets
- Established connections
- TIME-WAIT connections

---

### 10.18 Quick Diagnostic Command Set

For a quick network investigation, run:

```bash
ip addr
ip route
ip -s link
ip neigh show
ping -c 4 8.8.8.8
ping -c 4 google.com
nslookup google.com
ss -tulpn
curl -I https://google.com
```

If the problem is still not identified:

```bash
traceroute google.com
sudo tcpdump -i any
```

---

### Network Diagnostic Tool Summary

| Tool | Purpose |
|------|---------|
| `ip` | Interface, IP, routing, and neighbor information |
| `ping` | Test network connectivity |
| `nslookup` | DNS troubleshooting |
| `dig` | Detailed DNS troubleshooting |
| `traceroute` | Trace network path |
| `tracepath` | Trace network path |
| `ss` | Check network connections and ports |
| `nc` | Test port connectivity |
| `curl` | Test HTTP/HTTPS connectivity |
| `tcpdump` | Capture network traffic |
| `ip neigh` | Check ARP/neighbor table |
| `systemctl` | Check network services |
| `journalctl` | Check service logs |
| `sar` | Monitor network statistics |

---

### Practical Troubleshooting Example

#### Problem

A server cannot connect to an application running on another server.

#### Investigation

```bash
ip addr
```

Check the local IP configuration.

```bash
ip route
```

Check the routing table and default gateway.

```bash
ping -c 4 <server-ip>
```

Test basic connectivity.

```bash
nc -zv <server-ip> 443
```

Test whether TCP port 443 is reachable.

```bash
curl -v https://<server-ip>
```

Test the application connection.

```bash
sudo tcpdump -i any host <server-ip>
```

Capture packets if further investigation is required.

#### Conclusion

Using multiple diagnostic tools helps identify whether the problem is related to:

- Network interface
- IP configuration
- Routing
- DNS
- Firewall
- Port connectivity
- Application service
- Packet transmission

---

### Key Takeaway

A network engineer should not depend on a single command.

Use multiple tools together to move from:

```text
Interface
   ↓
IP Address
   ↓
Routing
   ↓
DNS
   ↓
Connectivity
   ↓
Port
   ↓
Service
   ↓
Packets
   ↓
Root Cause
```

---

## 11. Network Performance Troubleshooting

Network connectivity may be available while applications still experience slow response, high latency, packet loss, or unstable connections.

This section covers how to identify common network performance problems.

### 11.1 Check Latency

Latency is the time required for a packet to travel from the source to the destination.

Use `ping` to measure latency:

```bash
ping -c 4 8.8.8.8
```

Example output:

```text
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=20.5 ms
```

The `time` value represents the approximate round-trip latency.

Check for:

- High response time
- Increasing latency
- Packet loss
- Unstable response times

---

### 11.2 Check Packet Loss

Packet loss occurs when packets fail to reach their destination.

Run:

```bash
ping -c 20 8.8.8.8
```

Example:

```text
20 packets transmitted, 20 received, 0% packet loss
```

Check for:

- `0% packet loss` → No packet loss detected
- Low packet loss → Possible network instability
- High packet loss → Possible network or infrastructure problem

---

### 11.3 Check Network Interface Errors

Check interface statistics:

```bash
ip -s link
```

Look for:

```text
RX errors
TX errors
dropped
overruns
carrier
```

High error or drop counters may indicate:

- Interface problems
- Network congestion
- Driver issues
- Hardware problems
- Link problems

---

### 11.4 Check Network Throughput

Network throughput is the amount of data transferred over the network within a given period.

Check interface statistics:

```bash
ip -s link
```

You can also use:

```bash
sar -n DEV 1 5
```

Look for:

- Receive traffic
- Transmit traffic
- Packets per second
- Interface utilization
- Errors

---

### 11.5 Check Interface Status and Speed

Use:

```bash
ip link
```

If `ethtool` is available:

```bash
sudo ethtool eth0
```

Check for:

- Link detected
- Speed
- Duplex
- Auto-negotiation
- Interface state

Example:

```text
Speed: 1000Mb/s
Duplex: Full
Link detected: yes
```

---

### 11.6 Check for Network Congestion

Network congestion occurs when traffic exceeds available network capacity.

Possible symptoms:

- High latency
- Packet loss
- Slow application response
- Retransmissions
- Increased interface utilization

Check interface statistics:

```bash
ip -s link
```

Check network activity:

```bash
sar -n DEV 1 5
```

Check active connections:

```bash
ss -s
```

---

### 11.7 Check TCP Connections

View TCP connections:

```bash
ss -tan
```

View listening TCP ports:

```bash
ss -ltn
```

View established connections:

```bash
ss -tan state established
```

Look for:

- Large number of connections
- Many `TIME-WAIT` connections
- Unexpected connections
- Connection buildup

---

### 11.8 Check TCP Retransmissions

TCP retransmissions occur when packets need to be sent again because they were lost or not acknowledged.

Use:

```bash
ss -s
```

For detailed packet analysis:

```bash
sudo tcpdump -i any tcp
```

Possible causes include:

- Packet loss
- Network congestion
- High latency
- Unstable network path
- Server overload

---

### 11.9 Check the Network Path

Use:

```bash
traceroute <destination>
```

Example:

```bash
traceroute google.com
```

If available:

```bash
mtr google.com
```

`mtr` combines the functionality of `ping` and `traceroute` and can continuously monitor latency and packet loss across network hops.

Check for:

- High latency at a specific hop
- Packet loss
- Unstable routes
- Routing problems

---

### 11.10 Compare Local and Remote Connectivity

Test the local gateway first:

```bash
ping -c 4 <gateway-ip>
```

Then test a public IP:

```bash
ping -c 4 8.8.8.8
```

Then test a hostname:

```bash
ping -c 4 google.com
```

This helps isolate the problem.

Example:

```text
Gateway works
     ↓
8.8.8.8 works
     ↓
google.com fails
     ↓
Possible DNS problem
```

---

### 11.11 Check DNS Response Time

Use:

```bash
dig google.com
```

Look for:

```text
Query time:
```

Example:

```text
;; Query time: 25 msec
```

High DNS response time can contribute to slow application startup and website access.

---

### 11.12 Check Application Response Time

Use `curl` to inspect HTTP connection timing:

```bash
curl -o /dev/null -s -w "DNS: %{time_namelookup}s\nConnect: %{time_connect}s\nStart Transfer: %{time_starttransfer}s\nTotal: %{time_total}s\n" https://google.com
```

This helps identify whether the delay occurs during:

- DNS lookup
- TCP connection
- Server response
- Data transfer

---

### 11.13 Capture Traffic for Performance Analysis

Use `tcpdump`:

```bash
sudo tcpdump -i any host <server-ip>
```

For TCP traffic:

```bash
sudo tcpdump -i any tcp host <server-ip>
```

Look for:

- Retransmissions
- Duplicate packets
- Connection resets
- Delayed responses
- TCP handshake problems

---

### 11.14 Common Performance Problems

| Problem | Possible Cause |
|--------|----------------|
| High latency | Long network path or congestion |
| Packet loss | Network instability or overloaded link |
| Slow DNS | DNS server or network problem |
| Slow application | Server or network delay |
| TCP retransmissions | Packet loss or congestion |
| Interface errors | Link, driver, or hardware issue |
| Connection buildup | Application or resource issue |
| Low throughput | Congestion, link limitation, or configuration |

---

### 11.15 Practical Performance Troubleshooting Flow

```text
Application is slow
        ↓
Check latency
        ↓
Check packet loss
        ↓
Check interface errors
        ↓
Check network utilization
        ↓
Check routing path
        ↓
Check DNS response
        ↓
Check TCP connections
        ↓
Capture packets if required
        ↓
Identify root cause
        ↓
Apply fix
        ↓
Verify performance
```

---

### 11.16 Example Troubleshooting Scenario

#### Problem

Users report that an application is responding slowly.

#### Step 1: Test latency

```bash
ping -c 10 <server-ip>
```

#### Step 2: Check packet loss

Review the ping output for packet loss.

#### Step 3: Check interface statistics

```bash
ip -s link
```

#### Step 4: Check routing

```bash
ip route
```

#### Step 5: Check network path

```bash
traceroute <server-ip>
```

#### Step 6: Test application response

```bash
curl -I http://<server-ip>
```

#### Step 7: Capture traffic if required

```bash
sudo tcpdump -i any host <server-ip>
```

#### Conclusion

The investigation should determine whether the performance issue is caused by:

- High latency
- Packet loss
- Network congestion
- DNS delay
- Routing problems
- TCP retransmissions
- Server-side performance
- Application-level issues

---

### Key Takeaway

Network connectivity alone does not guarantee good performance.

A network engineer should investigate:

```text
Latency
   ↓
Packet Loss
   ↓
Errors
   ↓
Throughput
   ↓
Routing
   ↓
DNS
   ↓
TCP Connections
   ↓
Application Response
   ↓
Root Cause
```

---


## 12. Practical Troubleshooting Case Studies

This section demonstrates practical approaches to diagnosing common Linux networking problems.

### Case Study 1: Server Has No Network Connectivity

#### Problem

A Linux server cannot access the network.

#### Investigation

Check the interface:

```bash
ip link
```

Check the IP address:

```bash
ip addr
```

Check the routing table:

```bash
ip route
```

Test the default gateway:

```bash
ping -c 4 <gateway-ip>
```

Test external connectivity:

```bash
ping -c 4 8.8.8.8
```

#### Possible Causes

- Network interface is DOWN
- IP address is missing
- Incorrect subnet configuration
- Default gateway is missing
- Routing problem
- Firewall restriction

#### Resolution Approach

Verify the interface, IP configuration, default gateway, and routing table before checking external connectivity.

---

### Case Study 2: DNS Resolution Failure

#### Problem

The server can reach an IP address but cannot resolve domain names.

#### Investigation

Test IP connectivity:

```bash
ping -c 4 8.8.8.8
```

Test hostname resolution:

```bash
ping -c 4 google.com
```

Check DNS configuration:

```bash
cat /etc/resolv.conf
```

Test DNS directly:

```bash
nslookup google.com
```

Use `dig` for detailed information:

```bash
dig google.com
```

#### Possible Causes

- Incorrect DNS server
- DNS server unavailable
- DNS configuration problem
- Network connectivity to DNS server
- Firewall blocking DNS traffic

#### Resolution Approach

Verify DNS configuration and confirm that the configured DNS server is reachable.

---

### Case Study 3: Application Port Is Not Reachable

#### Problem

An application is running on a server, but clients cannot connect to its port.

#### Investigation

Check listening ports:

```bash
ss -ltnp
```

Check the specific port:

```bash
ss -ltnp | grep :443
```

Test the remote port:

```bash
nc -zv <server-ip> 443
```

Check firewall rules:

```bash
sudo ufw status
```

Check the service:

```bash
systemctl status <service-name>
```

#### Possible Causes

- Application is not running
- Application is listening on the wrong port
- Firewall is blocking the port
- Service is listening only on localhost
- Network connectivity problem

#### Resolution Approach

Verify the service status, listening address, port, firewall rules, and network connectivity.

---

### Case Study 4: High Network Latency

#### Problem

Users report that an application is responding slowly.

#### Investigation

Test latency:

```bash
ping -c 10 <server-ip>
```

Check the network path:

```bash
traceroute <server-ip>
```

Check interface statistics:

```bash
ip -s link
```

Check network activity:

```bash
sar -n DEV 1 5
```

#### Possible Causes

- Network congestion
- Long network path
- Packet loss
- Interface errors
- Routing problems
- Server performance issues

#### Resolution Approach

Compare latency across different network points and investigate the hop or interface where the problem begins.

---

### Case Study 5: Packet Loss

#### Problem

Network connections are unstable and packets are being lost.

#### Investigation

Run:

```bash
ping -c 20 <server-ip>
```

Check interface statistics:

```bash
ip -s link
```

Trace the network path:

```bash
traceroute <server-ip>
```

Capture traffic if required:

```bash
sudo tcpdump -i any host <server-ip>
```

#### Possible Causes

- Network congestion
- Faulty interface
- Packet drops
- Routing problems
- Unstable network path
- Hardware or link issues

#### Resolution Approach

Identify where packet loss begins and investigate the affected interface, route, or network segment.

---

### Case Study 6: Service Is Running but Connection Fails

#### Problem

The application service appears to be running, but clients cannot connect.

#### Investigation

Check service status:

```bash
systemctl status <service-name>
```

Check listening ports:

```bash
ss -ltnp
```

Check the listening address:

```bash
ss -ltnp | grep :<port>
```

Test locally:

```bash
curl http://localhost:<port>
```

Test remotely:

```bash
nc -zv <server-ip> <port>
```

Check firewall:

```bash
sudo ufw status
```

#### Possible Causes

- Service bound only to localhost
- Incorrect listening port
- Firewall restriction
- Application configuration problem
- Network connectivity issue

#### Resolution Approach

Compare local and remote connectivity and verify the application's listening address and firewall configuration.

---

### Case Study 7: Troubleshooting with tcpdump

#### Problem

A server sends requests but does not appear to receive responses.

#### Investigation

Capture traffic:

```bash
sudo tcpdump -i any host <server-ip>
```

Capture TCP traffic:

```bash
sudo tcpdump -i any tcp host <server-ip>
```

Capture traffic for a specific port:

```bash
sudo tcpdump -i any port 443
```

#### Look For

- TCP SYN packets
- SYN-ACK responses
- TCP retransmissions
- Connection resets
- ICMP errors
- Missing responses

#### Resolution Approach

Use packet capture to determine whether packets are leaving the host and whether responses are returning.

---

### Troubleshooting Method

For each network problem:

```text
Identify the Problem
        ↓
Collect Information
        ↓
Check Interface
        ↓
Check IP Configuration
        ↓
Check Routing
        ↓
Check DNS
        ↓
Test Connectivity
        ↓
Check Ports
        ↓
Check Firewall
        ↓
Check Service
        ↓
Capture Traffic if Required
        ↓
Identify Root Cause
        ↓
Apply Fix
        ↓
Verify the Fix
        ↓
Document the Resolution
```

### Key Takeaway

Effective network troubleshooting should be systematic and evidence-based.

The goal is to identify the **root cause** instead of repeatedly applying changes without understanding the problem.

---

## 13. Network Troubleshooting Checklist & Quick Reference

This section provides a quick checklist for troubleshooting common Linux network issues.

### 13.1 Network Interface Checklist

Check network interfaces:

```bash
ip link
```

Check interface state and IP address:

```bash
ip addr
```

Check interface statistics:

```bash
ip -s link
```

Look for:

- Interface DOWN
- Missing IP address
- RX errors
- TX errors
- Dropped packets
- Packet loss

---

### 13.2 IP Configuration Checklist

Check IP addresses:

```bash
ip addr show
```

Check the subnet configuration:

```bash
ip addr
```

Check the default gateway:

```bash
ip route show default
```

Verify that the IP address and subnet match the expected network configuration.

---

### 13.3 Routing Checklist

Display the routing table:

```bash
ip route
```

Check the default route:

```bash
ip route show default
```

Test the route to a destination:

```bash
ip route get 8.8.8.8
```

Look for:

- Missing default route
- Incorrect gateway
- Incorrect interface
- Unexpected routes
- Routing conflicts

---

### 13.4 DNS Checklist

Check DNS configuration:

```bash
cat /etc/resolv.conf
```

Test hostname resolution:

```bash
nslookup google.com
```

Use `dig` for detailed DNS information:

```bash
dig google.com
```

Test DNS using the configured resolver:

```bash
getent hosts google.com
```

Look for:

- Incorrect DNS server
- DNS server unreachable
- DNS timeout
- DNS resolution failure
- Incorrect DNS configuration

---

### 13.5 Connectivity Checklist

Test the local gateway:

```bash
ping -c 4 <gateway-ip>
```

Test external IP connectivity:

```bash
ping -c 4 8.8.8.8
```

Test hostname connectivity:

```bash
ping -c 4 google.com
```

Test the network path:

```bash
traceroute google.com
```

---

### 13.6 Port Connectivity Checklist

Check listening ports:

```bash
ss -ltnp
```

Check a specific port:

```bash
ss -ltnp | grep :443
```

Test remote port connectivity:

```bash
nc -zv <server-ip> <port>
```

Test HTTP connectivity:

```bash
curl -I http://<server-ip>
```

Look for:

- Port not listening
- Service stopped
- Firewall blocking traffic
- Incorrect port
- Service bound to localhost

---

### 13.7 Firewall Checklist

Check UFW status:

```bash
sudo ufw status
```

Check iptables rules:

```bash
sudo iptables -L -n -v
```

Check nftables rules:

```bash
sudo nft list ruleset
```

Look for:

- DROP rules
- REJECT rules
- Blocked ports
- Incorrect firewall configuration

---

### 13.8 Service Checklist

Check service status:

```bash
systemctl status <service-name>
```

Check whether a service is enabled:

```bash
systemctl is-enabled <service-name>
```

Check recent service logs:

```bash
journalctl -u <service-name> --since "10 minutes ago"
```

Look for:

- Service stopped
- Service failed
- Configuration errors
- Permission errors
- Dependency failures

---

### 13.9 Network Traffic Checklist

Capture network traffic:

```bash
sudo tcpdump -i any
```

Capture traffic for a specific host:

```bash
sudo tcpdump -i any host <server-ip>
```

Capture traffic for a specific port:

```bash
sudo tcpdump -i any port 443
```

Look for:

- TCP SYN packets
- SYN-ACK responses
- Retransmissions
- Connection resets
- ICMP errors
- Missing responses

---

### 13.10 ARP / Neighbor Checklist

Display the neighbor table:

```bash
ip neigh show
```

Check whether the gateway has been resolved:

```bash
ip neigh show <gateway-ip>
```

Look for:

- FAILED
- INCOMPLETE
- STALE
- Missing neighbor entry

---

### 13.11 Performance Checklist

Check network interface statistics:

```bash
ip -s link
```

Check network activity:

```bash
sar -n DEV 1 5
```

Check active connections:

```bash
ss -s
```

Test latency:

```bash
ping -c 10 <server-ip>
```

Look for:

- High latency
- Packet loss
- Interface errors
- Dropped packets
- High network utilization

---

### 13.12 Quick Troubleshooting Flow

```text
1. Identify the Problem
        ↓
2. Check Network Interface
        ↓
3. Check IP Address
        ↓
4. Check Default Gateway
        ↓
5. Check Routing
        ↓
6. Check DNS
        ↓
7. Test Connectivity
        ↓
8. Check Ports
        ↓
9. Check Firewall
        ↓
10. Check Service
        ↓
11. Check Logs
        ↓
12. Capture Traffic if Required
        ↓
13. Identify Root Cause
        ↓
14. Apply Fix
        ↓
15. Verify the Fix
        ↓
16. Document the Resolution
```

### Quick Command Reference

| Purpose | Command |
|---|---|
| Show interfaces | `ip link` |
| Show IP address | `ip addr` |
| Show routes | `ip route` |
| Show default route | `ip route show default` |
| Test connectivity | `ping` |
| Trace network path | `traceroute` |
| DNS lookup | `nslookup` |
| Detailed DNS lookup | `dig` |
| Show listening ports | `ss -ltnp` |
| Test port | `nc -zv` |
| Show neighbor table | `ip neigh` |
| Check firewall | `sudo ufw status` |
| Check service | `systemctl status` |
| View logs | `journalctl` |
| Capture traffic | `tcpdump` |
| Check interface errors | `ip -s link` |

### Key Takeaway

A structured troubleshooting checklist helps reduce investigation time and prevents important checks from being missed.

Always collect evidence, identify the root cause, apply the appropriate fix, verify the result, and document the resolution.

---

---

## 14. Network Security Troubleshooting

This section covers basic Linux network security checks used to identify firewall, port, access, and connection-related problems.

### 14.1 Check Firewall Status

Check UFW status:

```bash
sudo ufw status
```

Check detailed UFW rules:

```bash
sudo ufw status verbose
```

Check iptables rules:

```bash
sudo iptables -L -n -v
```

Check nftables rules:

```bash
sudo nft list ruleset
```

Look for:

- DROP rules
- REJECT rules
- Blocked ports
- Unexpected firewall rules
- Incorrect source or destination restrictions

---

### 14.2 Check Listening Services

Display listening TCP and UDP ports:

```bash
ss -lntup
```

Check a specific port:

```bash
ss -lntup | grep :443
```

Identify the process using a port:

```bash
sudo lsof -i :443
```

Look for:

- Unexpected open ports
- Required service not listening
- Service listening on the wrong address
- Unnecessary services exposed to the network

---

### 14.3 Check Listening Address

Check where a service is listening:

```bash
ss -lntp
```

Example:

```text
127.0.0.1:8080
```

The service is listening only on localhost.

Example:

```text
0.0.0.0:8080
```

The service is listening on all IPv4 interfaces.

Look for:

- Service bound only to localhost
- Incorrect IP address
- Incorrect port
- Unexpected public exposure

---

### 14.4 Test Port Access

Test whether a remote port is reachable:

```bash
nc -zv <server-ip> <port>
```

Example:

```bash
nc -zv 192.168.1.10 443
```

Test HTTP:

```bash
curl -I http://<server-ip>:<port>
```

Test HTTPS:

```bash
curl -I https://<server-ip>:<port>
```

Possible results:

```text
Connection succeeded
```

or:

```text
Connection refused
```

or:

```text
Connection timed out
```

These results can help determine whether the problem is related to the service, firewall, or network path.

---

### 14.5 Check SSH Connectivity

Test SSH connectivity:

```bash
ssh <user>@<server-ip>
```

Check whether SSH is listening:

```bash
ss -lntp | grep :22
```

Check SSH service:

```bash
systemctl status ssh
```

On some distributions:

```bash
systemctl status sshd
```

Check SSH logs:

```bash
journalctl -u ssh --since "10 minutes ago"
```

Look for:

- SSH service stopped
- Port 22 blocked
- Authentication failures
- Connection timeout
- Firewall restrictions

---

### 14.6 Check Firewall Rules for a Specific Port

Search iptables rules:

```bash
sudo iptables -L INPUT -n -v | grep 443
```

Check UFW rules:

```bash
sudo ufw status numbered
```

Verify whether the required port is allowed.

Example:

```text
443/tcp ALLOW
```

If the required port is blocked, investigate the firewall rule before making changes.

---

### 14.7 Check Active Connections

Display active TCP connections:

```bash
ss -tan
```

Display established connections:

```bash
ss -tan state established
```

Display connection summary:

```bash
ss -s
```

Look for:

- Large number of connections
- Unexpected remote addresses
- Large number of TIME-WAIT connections
- Large number of SYN-RECV connections
- Connection spikes

---

### 14.8 Check Network Traffic

Capture traffic with tcpdump:

```bash
sudo tcpdump -i any
```

Capture traffic from a specific host:

```bash
sudo tcpdump -i any host <server-ip>
```

Capture traffic on a specific port:

```bash
sudo tcpdump -i any port 443
```

Capture TCP traffic:

```bash
sudo tcpdump -i any tcp
```

Look for:

- Unexpected traffic
- Connection attempts
- TCP retransmissions
- TCP resets
- ICMP errors
- Missing responses

---

### 14.9 Check for Unexpected Open Ports

List all listening ports:

```bash
sudo ss -lntup
```

Review each listening service and identify whether it is required.

Example questions:

```text
What service is using this port?
Is this service required?
Who should be able to access it?
Is the port exposed externally?
Is the firewall allowing unnecessary access?
```

---

### 14.10 Basic Network Security Troubleshooting Workflow

```text
Identify the Problem
        ↓
Check Listening Ports
        ↓
Check Service Status
        ↓
Check Firewall Rules
        ↓
Test Port Connectivity
        ↓
Check Active Connections
        ↓
Capture Network Traffic
        ↓
Identify the Root Cause
        ↓
Apply the Appropriate Fix
        ↓
Verify Connectivity
        ↓
Document the Resolution
```

### 14.11 Example Troubleshooting Scenario

#### Problem

A user cannot connect to an application running on port 443.

#### Step 1: Check the Service

```bash
systemctl status <service-name>
```

#### Step 2: Check the Port

```bash
ss -lntp | grep :443
```

#### Step 3: Check Firewall

```bash
sudo ufw status
```

#### Step 4: Test Connectivity

```bash
nc -zv <server-ip> 443
```

#### Step 5: Check Traffic

```bash
sudo tcpdump -i any port 443
```

#### Possible Causes

- Application is stopped
- Port 443 is not listening
- Firewall is blocking port 443
- Service is listening only on localhost
- Network path is unavailable

#### Resolution

Identify the exact failure point before making changes. After applying the fix, test the connection again.

---

### Key Takeaway

Network security troubleshooting should focus on understanding **what is listening, who can access it, and what traffic is being allowed or blocked**.

Avoid making unnecessary firewall changes. Always verify the existing configuration, identify the root cause, apply the minimum required change, and verify the result.

---

---

## 15. Linux Network Troubleshooting by OSI Layer

The OSI model provides a structured way to understand and troubleshoot network problems.

Using the OSI model helps narrow down the possible root cause instead of checking everything randomly.

### Layer 1 – Physical Layer

The Physical Layer deals with the physical connection and network interface.

#### Check interface status:

```bash
ip link
```

#### Check interface statistics:

```bash
ip -s link
```

#### If available, check Ethernet information:

```bash
sudo ethtool eth0
```

Check for:

- Interface DOWN
- Link not detected
- RX errors
- TX errors
- Dropped packets
- Speed or duplex problems

---

### Layer 2 – Data Link Layer

The Data Link Layer deals with MAC addresses, Ethernet communication, and local network neighbors.

#### Check MAC address:

```bash
ip link show
```

#### Check ARP / neighbor table:

```bash
ip neigh show
```

#### Test local gateway:

```bash
ping -c 4 <gateway-ip>
```

Check for:

- Missing neighbor entries
- FAILED neighbor state
- Incorrect MAC information
- Local network connectivity problems

---

### Layer 3 – Network Layer

The Network Layer deals with IP addressing and routing.

#### Check IP address:

```bash
ip addr
```

#### Check routing table:

```bash
ip route
```

#### Check default gateway:

```bash
ip route show default
```

#### Test route to a destination:

```bash
ip route get 8.8.8.8
```

Check for:

- Incorrect IP address
- Incorrect subnet
- Missing default gateway
- Incorrect routes
- Unreachable destination

---

### Layer 4 – Transport Layer

The Transport Layer deals mainly with TCP and UDP communication and ports.

#### Check listening ports:

```bash
ss -lntup
```

#### Check active connections:

```bash
ss -tan
```

#### Test a remote TCP port:

```bash
nc -zv <server-ip> <port>
```

Example:

```bash
nc -zv 192.168.1.10 443
```

Check for:

- Port not listening
- Connection refused
- Connection timeout
- Firewall restrictions
- Unexpected connections

---

### Layer 5 – Session Layer

The Session Layer deals with maintaining communication sessions between systems and applications.

For Linux troubleshooting, inspect active connections and service state.

#### Check established connections:

```bash
ss -tan state established
```

#### Check service status:

```bash
systemctl status <service-name>
```

#### Check service logs:

```bash
journalctl -u <service-name> --since "10 minutes ago"
```

Check for:

- Sessions being terminated
- Service restarts
- Connection failures
- Authentication problems
- Timeout issues

---

### Layer 6 – Presentation Layer

The Presentation Layer deals with data formatting, encryption, and encoding.

For network troubleshooting, HTTPS/TLS is a common example.

#### Test HTTPS:

```bash
curl -I https://google.com
```

#### View detailed HTTPS connection information:

```bash
curl -v https://google.com
```

Check for:

- TLS errors
- Certificate problems
- Protocol mismatches
- Encryption-related failures

---

### Layer 7 – Application Layer

The Application Layer includes network applications and protocols such as DNS, HTTP, SSH, and other services.

#### Test DNS:

```bash
nslookup google.com
```

#### Detailed DNS query:

```bash
dig google.com
```

#### Test HTTP:

```bash
curl -I https://google.com
```

#### Test SSH:

```bash
ssh <user>@<server-ip>
```

#### Check application service:

```bash
systemctl status <service-name>
```

Check for:

- DNS failures
- HTTP errors
- Application errors
- Service failures
- Authentication problems

---

## OSI Layer Troubleshooting Summary

| OSI Layer | Main Area | Useful Commands |
|---|---|---|
| Layer 1 – Physical | Interface and link | `ip link`, `ethtool` |
| Layer 2 – Data Link | MAC / ARP | `ip neigh`, `ip link` |
| Layer 3 – Network | IP / Routing | `ip addr`, `ip route` |
| Layer 4 – Transport | TCP / UDP / Ports | `ss`, `nc` |
| Layer 5 – Session | Sessions / Services | `ss`, `systemctl`, `journalctl` |
| Layer 6 – Presentation | TLS / Encryption | `curl -v` |
| Layer 7 – Application | DNS / HTTP / SSH | `dig`, `nslookup`, `curl`, `ssh` |

---

## OSI-Based Troubleshooting Flow

```text
Network Problem
      ↓
Layer 1
Physical / Interface
      ↓
Layer 2
MAC / ARP / Local Network
      ↓
Layer 3
IP / Routing
      ↓
Layer 4
TCP / UDP / Ports
      ↓
Layer 5
Sessions / Services
      ↓
Layer 6
TLS / Encryption
      ↓
Layer 7
DNS / HTTP / Application
      ↓
Root Cause
      ↓
Fix
      ↓
Verify
```

---

## Practical Example

### Problem

A user cannot access an HTTPS application.

### Step 1 – Layer 1

Check the network interface:

```bash
ip link
```

### Step 2 – Layer 2

Check the neighbor table:

```bash
ip neigh show
```

### Step 3 – Layer 3

Check IP and routing:

```bash
ip addr
ip route
```

Test connectivity:

```bash
ping -c 4 <server-ip>
```

### Step 4 – Layer 4

Test port 443:

```bash
nc -zv <server-ip> 443
```

### Step 5 – Layer 5

Check the application service:

```bash
systemctl status <service-name>
```

### Step 6 – Layer 6

Check HTTPS/TLS:

```bash
curl -v https://<server-ip>
```

### Step 7 – Layer 7

Check DNS:

```bash
nslookup <domain-name>
dig <domain-name>
```

### Conclusion

Troubleshooting from lower layers to higher layers helps identify the exact point where communication is failing.

---

## Key Takeaway

The OSI model provides a structured troubleshooting approach:

```text
Physical
   ↓
Data Link
   ↓
Network
   ↓
Transport
   ↓
Session
   ↓
Presentation
   ↓
Application
```

Start with the simplest and lowest-level checks, then move upward until the failure is identified.

---

## 16. Linux Networking Lab Summary

This lab provides practical experience with Linux networking, network troubleshooting, monitoring, and basic network security.

### Topics Covered

- Network Interfaces
- IP Configuration
- Routing
- DNS Troubleshooting
- Network Connectivity
- TCP and UDP Ports
- Network Troubleshooting Scenarios
- Troubleshooting Workflow
- Network Diagnostic Tools
- Network Performance Troubleshooting
- Practical Troubleshooting Case Studies
- Troubleshooting Checklists
- Network Security Troubleshooting
- OSI Layer Based Troubleshooting

---

### Important Commands Learned

```bash
ip addr
ip link
ip route
ip neigh
ping
traceroute
tracepath
nslookup
dig
ss
nc
curl
tcpdump
systemctl
journalctl
iptables
ufw
nft
sar
ethtool
```

---

### Troubleshooting Approach

The general approach used throughout this lab is:

```text
Identify the Problem
        ↓
Collect Information
        ↓
Check Interface
        ↓
Check IP Configuration
        ↓
Check Routing
        ↓
Check DNS
        ↓
Test Connectivity
        ↓
Check Ports
        ↓
Check Firewall
        ↓
Check Services
        ↓
Check Logs
        ↓
Capture Traffic if Required
        ↓
Identify Root Cause
        ↓
Apply Fix
        ↓
Verify the Fix
        ↓
Document the Resolution
```

---

### Skills Demonstrated

By completing this lab, the following practical skills are demonstrated:

- Linux network configuration
- IP addressing and subnet troubleshooting
- Routing troubleshooting
- DNS troubleshooting
- TCP/UDP connectivity testing
- Port troubleshooting
- Network performance analysis
- Packet capture and analysis
- Firewall troubleshooting
- Service and log analysis
- OSI-based troubleshooting
- Root cause analysis
- Network incident troubleshooting

---

### Real-World NOC / Network Engineer Application

The concepts and commands practiced in this lab can be applied to common NOC and Network Engineer activities such as:

- Investigating network alerts
- Troubleshooting server connectivity
- Checking DNS failures
- Investigating packet loss
- Troubleshooting application ports
- Checking firewall restrictions
- Investigating high latency
- Checking network interface errors
- Validating service availability
- Analyzing network traffic
- Documenting incidents and resolutions

---

### Final Troubleshooting Checklist

Before closing a network incident, verify:

```text
[ ] Network interface is UP
[ ] IP address is correct
[ ] Default gateway is available
[ ] Routing table is correct
[ ] DNS resolution works
[ ] Network connectivity works
[ ] Required port is reachable
[ ] Firewall rules are correct
[ ] Required service is running
[ ] Logs show no related errors
[ ] Network performance is acceptable
[ ] Fix has been verified
[ ] Incident has been documented
```

---

## Conclusion

This Linux Networking Lab was created to build practical troubleshooting skills using real Linux networking commands and structured troubleshooting methods.

The lab focuses on understanding the problem, collecting evidence, identifying the root cause, applying the appropriate fix, verifying the result, and documenting the resolution.

```text
Monitor
   ↓
Detect
   ↓
Investigate
   ↓
Troubleshoot
   ↓
Identify Root Cause
   ↓
Resolve
   ↓
Verify
   ↓
Document
```

**Linux Networking Lab — Completed.** ✅

---
