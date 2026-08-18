# TCP/IP Troubleshooting Lab

This section contains hands-on TCP/IP troubleshooting concepts, commands, scenarios, and practical exercises for NOC and network operations environments.

## Topics

- TCP/IP fundamentals
- TCP vs UDP
- OSI and TCP/IP models
- IP addressing
- IPv4
- IPv6
- Subnetting basics
- Private and public IP addresses
- Default gateway
- Ports and protocols
- TCP connection establishment
- TCP three-way handshake
- TCP connection termination
- Connectivity testing
- ICMP
- Ping
- Traceroute
- TCP connection testing
- `ss`
- `netstat`
- `curl`
- `nc`
- DNS and TCP/IP relationship
- Routing basics
- Network interface troubleshooting
- Common connectivity issues
- TCP timeout troubleshooting
- Connection refused troubleshooting
- Packet loss troubleshooting
- NOC troubleshooting workflow
- Practical scenarios
- Verification and documentation

---

## 1. TCP/IP Fundamentals

TCP/IP is a collection of networking protocols used for communication between systems over a network.

The TCP/IP model commonly consists of four layers:

```text
Application Layer
        ↓
Transport Layer
        ↓
Internet Layer
        ↓
Network Access Layer
```

### TCP/IP Model

| Layer | Examples |
|---|---|
| Application | HTTP, HTTPS, DNS, SSH, FTP |
| Transport | TCP, UDP |
| Internet | IPv4, IPv6, ICMP |
| Network Access | Ethernet, Wi-Fi, ARP |

---

## 2. TCP/IP Communication Flow

When a client communicates with a remote server:

```text
Client
  ↓
Network Interface
  ↓
Default Gateway
  ↓
Router
  ↓
Network
  ↓
Remote Router
  ↓
Server
```

Example:

```text
Client
192.168.1.10
     ↓
Gateway
192.168.1.1
     ↓
Internet
     ↓
Server
142.250.x.x
```

---

## 3. OSI Model vs TCP/IP Model

### OSI Model

```text
7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data Link
1. Physical
```

### TCP/IP Model

```text
Application
Transport
Internet
Network Access
```

### Important Mapping

```text
OSI Application
OSI Presentation
OSI Session
        ↓
TCP/IP Application

OSI Transport
        ↓
TCP/IP Transport

OSI Network
        ↓
TCP/IP Internet

OSI Data Link
OSI Physical
        ↓
TCP/IP Network Access
```

---

## 4. TCP vs UDP

TCP and UDP operate at the transport layer.

### TCP

TCP is connection-oriented.

Characteristics:

- Reliable
- Connection-oriented
- Ordered delivery
- Error detection
- Retransmission
- Flow control
- Congestion control

Common TCP applications:

```text
HTTP
HTTPS
SSH
FTP
SMTP
IMAP
```

### UDP

UDP is connectionless.

Characteristics:

- Faster
- No connection establishment
- No guaranteed delivery
- No retransmission
- Lower overhead

Common UDP applications:

```text
DNS
DHCP
NTP
VoIP
Streaming
```

### TCP vs UDP Comparison

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliability | Reliable | No delivery guarantee |
| Ordering | Maintains order | No guarantee |
| Retransmission | Yes | No |
| Speed | Generally slower | Generally faster |
| Overhead | Higher | Lower |
| Examples | HTTPS, SSH | DNS, DHCP |

---

## 5. IP Addressing

An IP address identifies a device or network interface on an IP network.

Example IPv4 address:

```text
192.168.1.10
```

An IPv4 address contains four octets.

```text
192 . 168 . 1 . 10
 ↓     ↓    ↓    ↓
Octet Octet Octet Octet
```

Each octet ranges from:

```text
0 - 255
```

---

## 6. IPv4 Address

IPv4 uses 32-bit addresses.

Example:

```text
192.168.1.10
```

Binary representation:

```text
11000000.10101000.00000001.00001010
```

IPv4 address structure:

```text
Network Portion + Host Portion
```

The subnet mask determines which portion represents the network and which portion represents the host.

---

## 7. Subnet Mask

Example:

```text
IP Address:
192.168.1.10

Subnet Mask:
255.255.255.0
```

CIDR notation:

```text
192.168.1.10/24
```

A `/24` means that the first 24 bits represent the network portion.

Example:

```text
Network:
192.168.1.0/24

Usable Host Range:
192.168.1.1 - 192.168.1.254

Broadcast:
192.168.1.255
```

---

## 8. Private IPv4 Address Ranges

Private IPv4 ranges include:

```text
10.0.0.0/8
```

```text
172.16.0.0/12
```

```text
192.168.0.0/16
```

Examples:

```text
10.10.10.10
172.16.5.20
192.168.1.100
```

These addresses are commonly used inside private networks.

---

## 9. Public IP Address

A public IP address is routable across the public Internet.

Example:

```text
142.250.x.x
```

Public IP addresses are commonly used by Internet-facing services.

---

## 10. Default Gateway

The default gateway is the router used by a host to reach networks outside its local subnet.

Example:

```text
Client:
192.168.1.10/24

Gateway:
192.168.1.1
```

Traffic to another network is sent through:

```text
192.168.1.1
```

Check routing information:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
```

---

## 11. Network Interface Information

List network interfaces:

```bash
ip link
```

Display IP addresses:

```bash
ip addr
```

Short form:

```bash
ip a
```

Display a specific interface:

```bash
ip addr show eth0
```

Display interface statistics:

```bash
ip -s link
```

---

## 12. Check Interface Status

Check whether an interface is up:

```bash
ip link show eth0
```

Look for:

```text
state UP
```

or:

```text
state DOWN
```

If an interface is down, connectivity may fail.

---

## 13. Bring an Interface Up

To bring an interface up:

```bash
sudo ip link set eth0 up
```

Bring an interface down:

```bash
sudo ip link set eth0 down
```

> Use interface changes carefully on production systems because they can interrupt connectivity.

---

## 14. Check Routing Table

Display routing information:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.10
```

The routing table determines where packets should be sent.

---

## 15. Routing Decision

Suppose the client has:

```text
IP:
192.168.1.10

Subnet:
192.168.1.0/24

Gateway:
192.168.1.1
```

If the destination is:

```text
192.168.1.20
```

The destination is on the local network.

If the destination is:

```text
10.10.10.20
```

The destination is on another network, so traffic is sent to the default gateway.

```text
Client
192.168.1.10
      ↓
Default Gateway
192.168.1.1
      ↓
Remote Network
10.10.10.0/24
```

---

## 16. TCP Ports

A port identifies a service or application endpoint.

Common ports:

| Port | Protocol | Service |
|---|---|---|
| 22 | TCP | SSH |
| 23 | TCP | Telnet |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 67 | UDP | DHCP Server |
| 68 | UDP | DHCP Client |
| 80 | TCP | HTTP |
| 110 | TCP | POP3 |
| 123 | UDP | NTP |
| 143 | TCP | IMAP |
| 443 | TCP | HTTPS |
| 3306 | TCP | MySQL |
| 5432 | TCP | PostgreSQL |
| 6379 | TCP | Redis |
| 8080 | TCP | Common Web Application |

---

## 17. TCP Connection

A TCP connection is identified by:

```text
Source IP
Source Port
Destination IP
Destination Port
Protocol
```

Example:

```text
Client:
192.168.1.10:52341

Server:
10.10.10.20:443

Protocol:
TCP
```

---

## 18. TCP Three-Way Handshake

TCP establishes a connection using a three-way handshake.

```text
Client                    Server
  |                         |
  | -------- SYN -------->  |
  |                         |
  | <------ SYN-ACK ------  |
  |                         |
  | -------- ACK -------->  |
  |                         |
  |     Connection Ready    |
```

### Step 1 — SYN

Client sends:

```text
SYN
```

The client requests a TCP connection.

### Step 2 — SYN-ACK

Server responds:

```text
SYN-ACK
```

The server acknowledges the request.

### Step 3 — ACK

Client sends:

```text
ACK
```

The TCP connection is established.

---

## 19. TCP Connection Termination

TCP normally uses FIN and ACK packets to close a connection.

Simplified flow:

```text
Client                    Server
  |                         |
  | -------- FIN -------->  |
  | <-------- ACK --------  |
  | <-------- FIN --------  |
  | -------- ACK -------->  |
  |                         |
  |      Connection Closed  |
```

---

## 20. TCP Connection States

Common TCP states include:

```text
LISTEN
SYN-SENT
SYN-RECEIVED
ESTABLISHED
FIN-WAIT-1
FIN-WAIT-2
TIME-WAIT
CLOSE-WAIT
LAST-ACK
CLOSED
```

Check TCP connections:

```bash
ss -tan
```

---

## 21. Using ss

`ss` is commonly used to inspect sockets and network connections.

Display TCP connections:

```bash
ss -t
```

Display listening TCP ports:

```bash
ss -ltn
```

Display UDP sockets:

```bash
ss -lun
```

Display TCP and UDP:

```bash
ss -tuln
```

Display process information:

```bash
sudo ss -tulpn
```

---

## 22. Using netstat

On systems where `netstat` is installed:

```bash
netstat -tuln
```

Display listening ports:

```bash
netstat -lnt
```

Display established connections:

```bash
netstat -nt
```

Display routing information:

```bash
netstat -rn
```

Modern Linux systems generally prefer `ss`.

---

## 23. Ping

`ping` uses ICMP to test IP-level connectivity.

Basic test:

```bash
ping 8.8.8.8
```

Test a hostname:

```bash
ping google.com
```

Send a limited number of packets:

```bash
ping -c 4 8.8.8.8
```

Example:

```text
64 bytes from 8.8.8.8:
icmp_seq=1
ttl=117
time=20 ms
```

---

## 24. Understanding Ping Results

Important fields include:

```text
icmp_seq
ttl
time
```

### icmp_seq

Sequence number of the ICMP packet.

### ttl

Time To Live value in the received packet.

### time

Round-trip time between the source and destination.

---

## 25. Packet Loss

Example:

```text
4 packets transmitted,
3 packets received,
25% packet loss
```

Packet loss can indicate:

- Network congestion
- Interface problems
- Wireless issues
- Routing problems
- Firewall behavior
- Remote host problems
- Network device issues

---

## 26. Ping Failure

If:

```bash
ping 8.8.8.8
```

fails, check:

```bash
ip addr
```

Then:

```bash
ip route
```

Then test the gateway:

```bash
ping <DEFAULT_GATEWAY>
```

If the gateway is unreachable, investigate local network connectivity.

---

## 27. Traceroute

Traceroute identifies the path packets take toward a destination.

Run:

```bash
traceroute google.com
```

On some Linux systems:

```bash
tracepath google.com
```

Traceroute can help identify where connectivity is failing.

---

## 28. Traceroute Example

Example:

```text
1  192.168.1.1
2  10.10.10.1
3  172.16.20.1
4  203.0.113.1
5  142.250.x.x
```

This represents the path through multiple network hops.

---

## 29. Traceroute Troubleshooting

If the trace stops at a particular hop:

```text
1  192.168.1.1
2  10.10.10.1
3  * * *
4  * * *
```

Possible causes include:

- ICMP filtering
- Firewall rules
- Routing problems
- Network device configuration
- Packet loss

A timeout at one hop does not always mean that the network is broken because some routers intentionally do not respond to traceroute probes.

---

## 30. TCP Connectivity Testing

Ping tests IP-level connectivity but does not confirm that a specific TCP service is reachable.

For example:

```bash
ping 10.10.10.20
```

may succeed while:

```text
TCP port 443
```

is unavailable.

Therefore, test the actual port.

---

## 31. Using nc

`nc` or netcat can test TCP connectivity.

Example:

```bash
nc -vz 10.10.10.20 443
```

Test SSH:

```bash
nc -vz 10.10.10.20 22
```

Test HTTP:

```bash
nc -vz 10.10.10.20 80
```

Successful output generally indicates that the TCP connection could be established.

---

## 32. Connection Refused

Example:

```text
Connection refused
```

This usually means:

```text
Host reachable
        ↓
TCP connection attempted
        ↓
Destination actively rejected connection
```

Possible causes:

- Service is not running
- Port is not listening
- Firewall rule rejects the connection
- Application is configured incorrectly

Check listening ports:

```bash
ss -ltn
```

---

## 33. Connection Timeout

Example:

```text
Connection timed out
```

Possible causes:

- Host unreachable
- Firewall silently dropping packets
- Routing problem
- Network ACL
- Security group
- Service unavailable
- Intermediate network problem

Test:

```bash
ping <SERVER_IP>
```

Then:

```bash
nc -vz <SERVER_IP> <PORT>
```

Then:

```bash
traceroute <SERVER_IP>
```

---

## 34. curl

`curl` is commonly used to test HTTP and HTTPS connectivity.

Test HTTP:

```bash
curl http://example.com
```

Test HTTPS:

```bash
curl https://example.com
```

Display only HTTP headers:

```bash
curl -I https://example.com
```

Verbose output:

```bash
curl -v https://example.com
```

The verbose option is useful for troubleshooting connection establishment, TLS negotiation, and HTTP communication.

---

## 35. curl Connectivity Workflow

Example:

```bash
curl -v https://example.com
```

Check:

```text
DNS resolution
      ↓
TCP connection
      ↓
TLS handshake
      ↓
HTTP request
      ↓
HTTP response
```

This makes `curl -v` useful for application connectivity troubleshooting.

---

## 36. DNS and TCP/IP Relationship

DNS and TCP/IP troubleshooting are closely related.

Example:

```text
Application
    ↓
DNS Resolution
    ↓
IP Address
    ↓
Routing
    ↓
TCP Connection
    ↓
Application Service
```

If DNS fails:

```text
hostname → IP address
```

cannot be completed.

If DNS works but TCP fails:

```text
IP address → TCP service
```

must be investigated.

---

## 37. Troubleshooting Layer by Layer

Use a layered approach:

```text
1. Application
        ↓
2. TCP/UDP Port
        ↓
3. IP Connectivity
        ↓
4. Routing
        ↓
5. Network Interface
        ↓
6. Physical/Network Connectivity
```

This prevents random troubleshooting.

---

## 38. Basic Connectivity Workflow

Start with the destination IP:

```bash
ping <DESTINATION_IP>
```

Check the local interface:

```bash
ip addr
```

Check the routing table:

```bash
ip route
```

Check the default gateway:

```bash
ip route | grep default
```

Test the gateway:

```bash
ping <DEFAULT_GATEWAY>
```

Test the application port:

```bash
nc -vz <DESTINATION_IP> <PORT>
```

Trace the route:

```bash
traceroute <DESTINATION_IP>
```

---

## 39. Local Network Troubleshooting

If the host cannot communicate with anything:

Check interface:

```bash
ip link
```

Check IP:

```bash
ip addr
```

Check gateway:

```bash
ip route
```

Test gateway:

```bash
ping <DEFAULT_GATEWAY>
```

If the gateway fails, investigate:

- Interface status
- IP configuration
- Subnet mask
- VLAN
- Local routing
- Physical connectivity

---

## 40. Remote Network Troubleshooting

If the local gateway is reachable but a remote server is not:

```text
Client
  ↓
Gateway
  ↓
Remote Network
  ↓
Server
```

Check:

```bash
ping <REMOTE_IP>
```

Then:

```bash
traceroute <REMOTE_IP>
```

Then:

```bash
nc -vz <REMOTE_IP> <PORT>
```

Possible causes:

- Routing issue
- Firewall
- ACL
- Security group
- Remote service unavailable

---

## 41. Common TCP/IP Problems

Common problems include:

- Incorrect IP address
- Incorrect subnet mask
- Incorrect gateway
- Interface down
- Routing failure
- Packet loss
- High latency
- DNS failure
- TCP port blocked
- Service not listening
- Firewall restriction
- Network ACL
- Security group
- Application failure

---

## 42. High Latency

Latency is the time required for packets to travel between endpoints.

Test:

```bash
ping -c 10 <DESTINATION_IP>
```

Look at:

```text
min
avg
max
```

Example:

```text
rtt min/avg/max = 10/15/25 ms
```

High latency may be caused by:

- Network congestion
- Long network path
- Routing changes
- Overloaded network devices
- Remote server load

---

## 43. Packet Loss Troubleshooting

Test:

```bash
ping -c 20 <DESTINATION_IP>
```

If packet loss occurs:

```text
Client
  ↓
Gateway
  ↓
Intermediate Hops
  ↓
Destination
```

Test the gateway first:

```bash
ping -c 20 <DEFAULT_GATEWAY>
```

Then test the remote destination:

```bash
ping -c 20 <DESTINATION_IP>
```

Compare the results.

---

## 44. Network Interface Errors

Display interface statistics:

```bash
ip -s link
```

Look for:

```text
RX errors
TX errors
dropped
overruns
```

Large or increasing error counters may indicate network or interface problems.

---

## 45. ARP Basics

ARP is used in IPv4 networks to map IP addresses to MAC addresses on the local network.

Display neighbor information:

```bash
ip neigh
```

Example:

```text
192.168.1.1 dev eth0 lladdr aa:bb:cc:dd:ee:ff REACHABLE
```

This shows the MAC address associated with the local gateway.

---

## 46. IPv6 Basics

IPv6 uses 128-bit addresses.

Example:

```text
2001:db8::10
```

IPv6 provides a much larger address space than IPv4.

Check IPv6 addresses:

```bash
ip -6 addr
```

Check IPv6 routes:

```bash
ip -6 route
```

Test IPv6 connectivity:

```bash
ping6 google.com
```

---

## 47. IPv4 vs IPv6

| Feature | IPv4 | IPv6 |
|---|---|---|
| Address size | 32-bit | 128-bit |
| Example | 192.168.1.10 | 2001:db8::10 |
| Address space | Smaller | Very large |
| Broadcast | Supported | Not used |
| Neighbor discovery | ARP | NDP |

---

## 48. Port Troubleshooting Workflow

Suppose an application is listening on port 443.

Check locally:

```bash
ss -ltnp | grep :443
```

Test remotely:

```bash
nc -vz <SERVER_IP> 443
```

Test the application:

```bash
curl -vk https://<SERVER_IP>
```

If the port is listening locally but inaccessible remotely, investigate:

- Firewall
- Security group
- Network ACL
- Routing
- Load balancer
- Network path

---

## 49. Practical Scenario 1 — Host Unreachable

### Problem

A NOC alert reports that a server is unreachable.

### Step 1

Check local network:

```bash
ip addr
```

### Step 2

Check routing:

```bash
ip route
```

### Step 3

Check gateway:

```bash
ping <DEFAULT_GATEWAY>
```

### Step 4

Check destination:

```bash
ping <SERVER_IP>
```

### Step 5

Trace route:

```bash
traceroute <SERVER_IP>
```

### Possible Root Causes

```text
Interface down
Incorrect IP configuration
Incorrect gateway
Routing failure
Firewall
Remote server issue
```

---

## 50. Practical Scenario 2 — Port 443 Unreachable

### Problem

The server is reachable, but HTTPS is not working.

Test:

```bash
ping <SERVER_IP>
```

If successful:

```bash
nc -vz <SERVER_IP> 443
```

Then:

```bash
curl -vk https://<SERVER_IP>
```

Check server listening ports:

```bash
ss -ltnp | grep :443
```

### Possible Root Causes

```text
HTTPS service stopped
Port 443 not listening
Firewall blocking port 443
Security group restriction
Application issue
```

---

## 51. Practical Scenario 3 — Connection Refused

### Problem

An application reports:

```text
Connection refused
```

Test:

```bash
nc -vz <SERVER_IP> <PORT>
```

Check whether the service is listening:

```bash
ss -ltnp
```

Search for the required port:

```bash
ss -ltnp | grep :<PORT>
```

### Possible Root Cause

The service may not be running or listening on the expected port.

---

## 52. Practical Scenario 4 — Connection Timeout

### Problem

An application reports:

```text
Connection timed out
```

Test:

```bash
ping <SERVER_IP>
```

Then:

```bash
traceroute <SERVER_IP>
```

Then:

```bash
nc -vz <SERVER_IP> <PORT>
```

### Possible Causes

```text
Routing problem
Firewall drop
Network ACL
Security group
Server unreachable
Network path issue
```

---

## 53. Practical Scenario 5 — High Latency

### Problem

Users report that an application is slow.

Test:

```bash
ping -c 20 <SERVER_IP>
```

Check route:

```bash
traceroute <SERVER_IP>
```

Test application:

```bash
curl -v https://<SERVER_IP>
```

Compare latency between:

```text
Client → Gateway
Client → Remote Server
```

If gateway latency is normal but remote latency is high, investigate the remote network path.

---

## 54. Practical Scenario 6 — Packet Loss

### Problem

A monitoring system reports packet loss.

Run:

```bash
ping -c 50 <SERVER_IP>
```

Check interface statistics:

```bash
ip -s link
```

Check gateway:

```bash
ping -c 50 <DEFAULT_GATEWAY>
```

Run:

```bash
traceroute <SERVER_IP>
```

### Possible Causes

- Interface errors
- Network congestion
- Routing issue
- Wireless instability
- Firewall behavior
- Remote host issue

---

## 55. Practical Scenario 7 — DNS Works but Application Fails

### Problem

Hostname resolution works:

```bash
nslookup application.example.com
```

But application access fails.

Check IP:

```bash
dig application.example.com +short
```

Test IP connectivity:

```bash
ping <RESOLVED_IP>
```

Test TCP:

```bash
nc -vz <RESOLVED_IP> 443
```

Test application:

```bash
curl -vk https://application.example.com
```

### Troubleshooting Logic

```text
DNS works
   ↓
IP connectivity works
   ↓
TCP port fails
   ↓
Investigate firewall / service / routing
```

---

## 56. Practical Scenario 8 — IP Works but Hostname Fails

### Problem

The application works using an IP address but not the hostname.

Test:

```bash
curl http://<SERVER_IP>
```

Then:

```bash
curl http://application.example.com
```

Check DNS:

```bash
nslookup application.example.com
```

Possible causes:

- DNS failure
- Incorrect DNS record
- DNS cache
- `/etc/hosts` issue
- Application hostname configuration

---

## 57. Practical Scenario 9 — Service Listening Locally but Remote Connection Fails

Check:

```bash
ss -ltnp | grep :8080
```

If the service is listening:

```text
0.0.0.0:8080
```

it may accept connections on all IPv4 interfaces.

If it is listening only on:

```text
127.0.0.1:8080
```

the service may accept only local connections.

Test locally:

```bash
curl http://127.0.0.1:8080
```

Then test remotely:

```bash
curl http://<SERVER_IP>:8080
```

---

## 58. NOC Troubleshooting Workflow

Use the following workflow for TCP/IP incidents:

```text
1. Identify the affected host
        ↓
2. Identify source and destination
        ↓
3. Check network interface
        ↓
4. Check IP configuration
        ↓
5. Check routing table
        ↓
6. Test default gateway
        ↓
7. Test destination IP
        ↓
8. Test TCP/UDP port
        ↓
9. Check application/service
        ↓
10. Check firewall or security controls
        ↓
11. Verify recovery
        ↓
12. Document findings
```

---

## 59. NOC Incident Investigation Template

Use this format when documenting a TCP/IP incident:

```text
Incident:
TCP/IP connectivity issue

Source Host:
<source hostname/IP>

Destination:
<destination hostname/IP>

Destination Port:
<port>

Symptoms:
<brief description>

Initial Test:
<command>

Network Test:
<command>

TCP Test:
<command>

Findings:
<observed result>

Root Cause:
<root cause>

Resolution:
<action taken>

Verification:
<verification performed>

Status:
Resolved / Monitoring
```

---

## 60. NOC Troubleshooting Commands Cheat Sheet

```bash
ip addr
ip link
ip -s link
ip route
ip neigh

ping <IP>
ping -c 4 <IP>

traceroute <IP>
tracepath <IP>

ss -t
ss -ltn
ss -lun
ss -tuln
sudo ss -tulpn

netstat -tuln
netstat -rn

nc -vz <IP> <PORT>

curl -I https://example.com
curl -v https://example.com

ip -6 addr
ip -6 route
ping6 google.com
```

---

## 61. Troubleshooting Decision Tree

```text
Application unavailable
        ↓
Can hostname resolve?
        ↓
      Yes
        ↓
Can IP be reached?
        ↓
      Yes
        ↓
Can TCP port connect?
        ↓
      Yes
        ↓
Is application responding?
        ↓
      No
        ↓
Investigate application/service
```

If hostname resolution fails:

```text
Check DNS
```

If IP connectivity fails:

```text
Check interface
Check gateway
Check routing
Check network path
```

If TCP connection fails:

```text
Check port
Check service
Check firewall
Check security controls
```

---

## 62. Verification Checklist

After completing this lab, verify that you can:

- [ ] Explain the TCP/IP model
- [ ] Explain TCP vs UDP
- [ ] Explain IPv4 addressing
- [ ] Explain IPv6 addressing
- [ ] Understand subnet masks
- [ ] Identify private IP ranges
- [ ] Identify public IP addresses
- [ ] Explain the default gateway
- [ ] Read the routing table
- [ ] Check network interfaces
- [ ] Check TCP listening ports
- [ ] Explain the TCP three-way handshake
- [ ] Explain TCP connection termination
- [ ] Use `ping`
- [ ] Use `traceroute`
- [ ] Use `ss`
- [ ] Use `netstat`
- [ ] Use `nc`
- [ ] Use `curl`
- [ ] Check ARP/neighbor information
- [ ] Troubleshoot packet loss
- [ ] Troubleshoot high latency
- [ ] Troubleshoot connection timeout
- [ ] Troubleshoot connection refused
- [ ] Troubleshoot port connectivity
- [ ] Troubleshoot routing issues
- [ ] Document a TCP/IP incident

---

## 63. Practical Exercises

### Exercise 1 — Identify IP Configuration

Run:

```bash
ip addr
```

Document:

```text
Interface:
IPv4 Address:
IPv6 Address:
```

### Exercise 2 — Identify Default Gateway

Run:

```bash
ip route
```

Identify:

```text
Default Gateway:
Interface:
```

### Exercise 3 — Test Gateway Connectivity

Run:

```bash
ping -c 4 <DEFAULT_GATEWAY>
```

Record:

```text
Packet Loss:
Average Latency:
```

### Exercise 4 — Test Internet Connectivity

Run:

```bash
ping -c 4 8.8.8.8
```

Record the result.

### Exercise 5 — Test DNS Connectivity

Run:

```bash
ping -c 4 google.com
```

Compare the result with Exercise 4.

### Exercise 6 — Trace the Network Path

Run:

```bash
traceroute google.com
```

Identify the first few hops.

### Exercise 7 — Check Listening Ports

Run:

```bash
ss -ltn
```

Identify the listening TCP ports.

### Exercise 8 — Test HTTPS Port

Run:

```bash
nc -vz google.com 443
```

Record whether the connection succeeds.

### Exercise 9 — Test HTTP/HTTPS

Run:

```bash
curl -I https://google.com
```

Record the HTTP response status.

### Exercise 10 — Inspect Network Statistics

Run:

```bash
ip -s link
```

Check:

```text
RX packets
TX packets
RX errors
TX errors
Dropped packets
```

---

## 64. TCP/IP Incident Example

### Alert

```text
Server connectivity check failed.
```

### Investigation

Check interface:

```bash
ip addr
```

Check route:

```bash
ip route
```

Test gateway:

```bash
ping -c 4 <DEFAULT_GATEWAY>
```

Test destination:

```bash
ping -c 4 <SERVER_IP>
```

Test application port:

```bash
nc -vz <SERVER_IP> 443
```

Check route:

```bash
traceroute <SERVER_IP>
```

### Findings

```text
Local interface is UP.
IP configuration is correct.
Default gateway is reachable.
Remote server is reachable.
TCP port 443 is not accepting connections.
```

### Root Cause

```text
HTTPS service was unavailable on the destination server.
```

### Resolution

```text
Responsible team restored the HTTPS service.
```

### Verification

```bash
nc -vz <SERVER_IP> 443
```

```bash
curl -vk https://<SERVER_IP>
```

### Status

```text
Resolved / Monitoring
```

---

## 65. TCP/IP Troubleshooting Best Practices

Always troubleshoot from the lowest relevant layer upward.

```text
Interface
   ↓
IP Address
   ↓
Gateway
   ↓
Routing
   ↓
Destination IP
   ↓
TCP Port
   ↓
Application
```

Avoid changing configuration immediately.

First collect evidence using:

```bash
ip addr
ip route
ping
traceroute
ss
nc
curl
```

Document every important finding.

---

## 66. Evidence Collection

For a NOC incident, capture:

```text
Timestamp
Source Host
Destination Host
Destination IP
Destination Port
Interface
IP Address
Default Gateway
Packet Loss
Latency
Traceroute
TCP Connection Result
Application Response
```

Example:

```text
Source:
noc-server01

Destination:
app-server01

Destination IP:
10.10.20.15

Port:
443

Ping:
Successful

Packet Loss:
0%

TCP 443:
Connection refused

Application:
HTTPS service unavailable
```

---

## 67. Final Verification

Before closing a TCP/IP incident, verify:

- [ ] Source host is healthy
- [ ] Network interface is UP
- [ ] IP address is correct
- [ ] Subnet is correct
- [ ] Default gateway is correct
- [ ] Routing table is correct
- [ ] Destination is reachable
- [ ] Required port is reachable
- [ ] Application is responding
- [ ] Packet loss is within acceptable limits
- [ ] Latency is acceptable
- [ ] Root cause is identified
- [ ] Resolution is documented
- [ ] Monitoring is normal

---

## Conclusion

This TCP/IP troubleshooting lab provides practical knowledge required for NOC and Network Operations environments.

The focus is on:

```text
TCP/IP Fundamentals
        +
IP Addressing
        +
Routing
        +
TCP and UDP
        +
Connectivity Testing
        +
Port Troubleshooting
        +
Network Failure Scenarios
        +
NOC Incident Documentation
```

These skills are directly applicable to network monitoring, incident troubleshooting, infrastructure support, and production operations environments.
