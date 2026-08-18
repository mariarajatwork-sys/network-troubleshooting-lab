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
