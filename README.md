# Kali-Linux-Firewall-Implementation
this is kali linux firewall implementation. i made it myself as a project of course and it also tells commands use to implement firewall.


# Kali Linux Firewall Configuration and Testing Lab

## Overview

This project demonstrates the implementation and testing of firewall rules on Kali Linux using iptables. The objective was to understand how Linux firewalls filter network traffic and how security policies can be enforced through packet filtering rules.

## Objectives

* Learn the fundamentals of Linux firewalls.
* Configure firewall rules using iptables.
* Understand packet filtering concepts.
* Test firewall behavior using networking tools.
* Verify rule effectiveness through practical experimentation.

## Environment

* Operating System: Kali Linux
* Firewall Tool: iptables
* Web Server: Python HTTP Server
* Testing Tools:

  * Nmap
  * curl
  * ping
  * ss

## Step 1: Start a Local Web Server

A simple HTTP server was created to generate network traffic for testing.

```bash
python3 -m http.server 8000
```

Verification:

```bash
ss -tuln | grep 8000
```

Expected Result:

```text
LISTEN 0 5 0.0.0.0:8000
```

## Step 2: Test Connectivity

The server was accessed locally using curl.

```bash
curl http://127.0.0.1:8000
```

Result:

The directory listing of the current folder was displayed, confirming that the server was accessible.

## Step 3: Configure Firewall Rule

An iptables rule was added to block incoming traffic on port 8000.

```bash
sudo iptables -A INPUT -p tcp --dport 8000 -j DROP
```

Rule Explanation:

* INPUT: Incoming traffic chain
* tcp: TCP protocol
* --dport 8000: Destination port 8000
* DROP: Silently discard packets

## Step 4: Verify Firewall Rules

The active firewall rules were displayed.

```bash
sudo iptables -L -n -v
```

This command shows:

* Rule counters
* Packet statistics
* Protocol information
* Firewall actions

## Step 5: Test Blocked Access

After applying the firewall rule, connectivity tests were repeated.

```bash
curl http://127.0.0.1:8000
```

Observation:

The firewall rule prevented access to the service according to the configured policy.

## Step 6: Remove Firewall Rule

The rule was removed to restore access.

```bash
sudo iptables -D INPUT -p tcp --dport 8000 -j DROP
```

Connectivity was tested again.

```bash
curl http://127.0.0.1:8000
```

The service became accessible once the blocking rule was removed.

## Concepts Learned

* Linux firewall architecture
* Packet filtering
* INPUT chain processing
* TCP/IP networking fundamentals
* Port-based access control
* Service exposure and protection
* Firewall rule management

## Skills Demonstrated

* Kali Linux administration
* iptables configuration
* Network troubleshooting
* Security testing
* Service management
* Command-line operations

## Future Improvements

* Configure rules for SSH access control.
* Implement source IP filtering.
* Explore nftables.
* Analyze traffic using Wireshark.
* Build a multi-VM attacker/target lab environment.

## Disclaimer

This project was performed in a controlled lab environment for educational purposes only.
