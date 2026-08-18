# DNS Troubleshooting Lab

This section contains hands-on DNS troubleshooting concepts, commands, scenarios, and practical exercises for Linux networking.

## Topics

- DNS fundamentals
- DNS resolution
- DNS records
- `/etc/resolv.conf`
- `/etc/hosts`
- `nslookup`
- `dig`
- `host`
- DNS query types
- DNS troubleshooting
- DNS connectivity
- Common DNS failures
- DNS troubleshooting workflow
- Practical scenarios
- Verification and documentation

---

## 1. DNS Fundamentals

DNS (Domain Name System) translates human-readable domain names into IP addresses.

For example:

```text
google.com
    ↓
DNS Resolution
    ↓
IP Address
```

DNS allows users and applications to access services using domain names instead of remembering IP addresses.

### DNS Resolution Flow

```text
Client
  ↓
Local DNS Cache
  ↓
DNS Resolver
  ↓
Root DNS Server
  ↓
TLD DNS Server
  ↓
Authoritative DNS Server
  ↓
IP Address
```

---

## 2. DNS Resolution

DNS resolution converts a hostname into an IP address.

Example:

```bash
ping google.com
```

Check DNS resolution using:

```bash
getent hosts google.com
```

```bash
nslookup google.com
```

```bash
dig google.com
```

```bash
host google.com
```

---

## 3. DNS Configuration

### `/etc/resolv.conf`

This file contains DNS resolver configuration.

Check the configuration:

```bash
cat /etc/resolv.conf
```

Example:

```text
nameserver 8.8.8.8
nameserver 1.1.1.1
```

Test DNS resolution:

```bash
nslookup google.com
```

> Note: `/etc/resolv.conf` may be managed automatically by NetworkManager, systemd-resolved, DHCP, or another network service.

---

## 4. `/etc/hosts`

The `/etc/hosts` file provides local hostname-to-IP mappings.

Check it:

```bash
cat /etc/hosts
```

Example:

```text
127.0.0.1       localhost
192.168.1.20    server01
192.168.1.30    database01
```

Test hostname resolution:

```bash
getent hosts server01
```

### Troubleshooting Example

If:

```bash
ping server01
```

fails, check:

```bash
cat /etc/hosts
```

The hostname may not have the expected IP mapping.

---

## 5. DNS Troubleshooting Commands

### nslookup

Basic DNS lookup:

```bash
nslookup google.com
```

Query a specific DNS server:

```bash
nslookup google.com 8.8.8.8
```

Reverse DNS lookup:

```bash
nslookup 8.8.8.8
```

### dig

Perform a DNS lookup:

```bash
dig google.com
```

Display only the IP address:

```bash
dig google.com +short
```

Query a specific DNS server:

```bash
dig @8.8.8.8 google.com
```

Query an A record:

```bash
dig google.com A
```

Query a CNAME record:

```bash
dig www.google.com CNAME
```

Query an MX record:

```bash
dig google.com MX
```

Query an NS record:

```bash
dig google.com NS
```

Reverse DNS lookup:

```bash
dig -x 8.8.8.8
```

### host

Basic DNS lookup:

```bash
host google.com
```

Reverse lookup:

```bash
host 8.8.8.8
```

Query a specific record:

```bash
host -t MX google.com
```

---

## 6. DNS Record Types

| Record | Purpose |
|---|---|
| A | Maps hostname to IPv4 address |
| AAAA | Maps hostname to IPv6 address |
| CNAME | Creates an alias for another hostname |
| MX | Defines mail servers |
| NS | Identifies authoritative DNS servers |
| TXT | Stores text-based information |
| PTR | Used for reverse DNS |
| SOA | Contains zone authority information |

### A Record

```bash
dig example.com A
```

### AAAA Record

```bash
dig example.com AAAA
```

### CNAME Record

```bash
dig www.example.com CNAME
```

### MX Record

```bash
dig example.com MX
```

### NS Record

```bash
dig example.com NS
```

### TXT Record

```bash
dig example.com TXT
```

---

## 7. DNS Connectivity Troubleshooting

DNS requires network connectivity to the DNS server.

First test basic connectivity:

```bash
ping 8.8.8.8
```

Then test hostname resolution:

```bash
ping google.com
```

### Scenario

If:

```bash
ping 8.8.8.8
```

works but:

```bash
ping google.com
```

fails, the problem may be related to DNS resolution.

Check:

```bash
cat /etc/resolv.conf
```

Then:

```bash
nslookup google.com
```

Then:

```bash
dig google.com
```

---

## 8. Common DNS Failures

### DNS Server Unreachable

Symptoms:

- DNS queries time out
- Websites cannot be resolved
- Applications cannot connect using hostnames

Check DNS server connectivity:

```bash
ping <DNS_SERVER_IP>
```

Test DNS:

```bash
nslookup google.com <DNS_SERVER_IP>
```

### Incorrect DNS Configuration

Check:

```bash
cat /etc/resolv.conf
```

Verify that the configured nameserver is correct.

### DNS Resolution Timeout

Test:

```bash
dig google.com
```

Possible causes:

- DNS server unavailable
- Network connectivity issue
- Firewall blocking DNS
- Incorrect DNS configuration

### NXDOMAIN

Example:

```text
status: NXDOMAIN
```

NXDOMAIN means the DNS server indicates that the requested domain does not exist.

Verify the hostname:

```bash
dig hostname.example.com
```

Check for spelling or DNS record issues.

### Wrong IP Address

If DNS resolves but returns an unexpected IP:

```bash
dig example.com
```

Check the returned A or AAAA records.

Possible causes:

- Incorrect DNS record
- DNS configuration change
- Stale DNS cache
- Load balancing or CDN behavior

---

## 9. DNS Troubleshooting Workflow

Use the following workflow when troubleshooting DNS issues:

```text
1. Identify the hostname
        ↓
2. Check basic network connectivity
        ↓
3. Check /etc/resolv.conf
        ↓
4. Check /etc/hosts
        ↓
5. Test DNS using nslookup
        ↓
6. Test DNS using dig
        ↓
7. Test a specific DNS server
        ↓
8. Check DNS record type
        ↓
9. Compare results from multiple DNS servers
        ↓
10. Document findings and resolution
```

---

## 10. Practical Scenario 1

### Problem

A server can reach an IP address but cannot access a website using its hostname.

Test:

```bash
ping 8.8.8.8
```

If successful, test:

```bash
ping google.com
```

If hostname resolution fails:

```bash
cat /etc/resolv.conf
```

Then:

```bash
nslookup google.com
```

Then:

```bash
dig google.com
```

Test another DNS server:

```bash
dig @8.8.8.8 google.com
```

### Possible Root Cause

DNS server configuration or DNS connectivity issue.

### Verification

If the external DNS server works while the default DNS server fails, investigate the configured DNS resolver.

---

## 11. Practical Scenario 2

### Problem

An internal application hostname is not resolving.

Example:

```bash
ping app-server
```

Check:

```bash
cat /etc/hosts
```

Then:

```bash
getent hosts app-server
```

Then:

```bash
nslookup app-server
```

If the hostname is expected to be resolved through DNS, verify the appropriate DNS server and DNS record.

---

## 12. Practical Scenario 3

### Problem

DNS queries are timing out.

Test:

```bash
dig google.com
```

Check the configured resolver:

```bash
cat /etc/resolv.conf
```

Test connectivity:

```bash
ping <DNS_SERVER_IP>
```

Test another DNS server:

```bash
dig @8.8.8.8 google.com
```

### Possible Causes

- DNS server unavailable
- Network connectivity issue
- Firewall restriction
- Incorrect DNS configuration
- DNS service failure

---

## 13. Practical Scenario 4

### Problem

A domain resolves to an unexpected IP address.

Run:

```bash
dig example.com +short
```

Check:

```bash
dig example.com A
```

Compare with another DNS resolver:

```bash
dig @8.8.8.8 example.com
```

Possible causes:

- DNS propagation
- DNS caching
- DNS record configuration
- CDN or load-balancing behavior

---

## 14. DNS Verification Checklist

Before closing a DNS incident, verify:

- [ ] Hostname is correct
- [ ] Network connectivity is working
- [ ] DNS server is reachable
- [ ] `/etc/resolv.conf` is correct
- [ ] `/etc/hosts` is correct
- [ ] DNS query succeeds
- [ ] Correct DNS record is returned
- [ ] Application connectivity is restored
- [ ] Results are documented

---

## 15. NOC Troubleshooting Example

### Alert

```text
Application hostname resolution failed.
```

### Investigation

```bash
cat /etc/resolv.conf
```

```bash
ping <DNS_SERVER_IP>
```

```bash
nslookup application.example.com
```

```bash
dig application.example.com
```

```bash
dig @8.8.8.8 application.example.com
```

### Findings

```text
Default DNS resolver failed to respond.
External DNS resolver responded successfully.
```

### Root Cause

```text
DNS resolver connectivity or service issue.
```

### Resolution

```text
DNS resolver service or connectivity was restored.
Hostname resolution was verified successfully.
```

### Verification

```bash
getent hosts application.example.com
```

```bash
ping application.example.com
```

---

## 16. NOC Incident Documentation

When documenting a DNS incident, capture:

```text
Incident:
DNS resolution failure

Affected Host:
<hostname>

DNS Server:
<DNS server IP>

Symptoms:
Hostname could not be resolved.

Commands Used:
- ping
- nslookup
- dig
- host
- getent

Root Cause:
<DNS/network/configuration issue>

Resolution:
<action taken>

Verification:
DNS resolution restored successfully.

Status:
Resolved / Monitoring
```

---

## 17. Key Commands Cheat Sheet

```bash
cat /etc/resolv.conf
cat /etc/hosts

getent hosts google.com

nslookup google.com
nslookup google.com 8.8.8.8

dig google.com
dig google.com +short
dig @8.8.8.8 google.com

dig google.com A
dig google.com AAAA
dig google.com MX
dig google.com NS
dig google.com TXT

dig -x 8.8.8.8

host google.com
host -t MX google.com
```

---

## 18. Practical Exercises

### Exercise 1

Find the DNS servers configured on your Linux system.

```bash
cat /etc/resolv.conf
```

### Exercise 2

Resolve Google's hostname.

```bash
nslookup google.com
```

### Exercise 3

Resolve Google's hostname using `dig`.

```bash
dig google.com
```

### Exercise 4

Display only the resolved IP address.

```bash
dig google.com +short
```

### Exercise 5

Query Google's A record.

```bash
dig google.com A
```

### Exercise 6

Perform a reverse DNS lookup.

```bash
dig -x 8.8.8.8
```

### Exercise 7

Query Google's MX records.

```bash
dig google.com MX
```

### Exercise 8

Query Google's NS records.

```bash
dig google.com NS
```

### Exercise 9

Compare DNS resolution using the default resolver and Google DNS.

```bash
dig google.com
```

```bash
dig @8.8.8.8 google.com
```

Document whether the results are the same or different.

---

## 19. Verification

After completing the exercises, verify that you can:

- [ ] Explain what DNS does
- [ ] Explain the DNS resolution process
- [ ] Identify DNS configuration
- [ ] Use `/etc/resolv.conf`
- [ ] Use `/etc/hosts`
- [ ] Use `nslookup`
- [ ] Use `dig`
- [ ] Use `host`
- [ ] Query different DNS record types
- [ ] Troubleshoot DNS timeout
- [ ] Troubleshoot NXDOMAIN
- [ ] Troubleshoot incorrect DNS resolution
- [ ] Compare DNS servers
- [ ] Document a DNS incident

---

## Conclusion

This DNS lab provides practical troubleshooting knowledge required for NOC and Network Operations environments.

The focus is on:

```text
DNS Fundamentals
        +
Linux DNS Configuration
        +
DNS Troubleshooting Commands
        +
Real-World Failure Scenarios
        +
NOC Incident Documentation
```

These skills are directly applicable to network monitoring, incident troubleshooting, and infrastructure support environments.
