# Task: Local Network Port Scan (Parrot OS)

## Tools Used:
- Nmap
- Wireshark

## Nmap:

Nmap (Network Mapper) is a free and open-source tool used for:

  -  Network discovery

  -  Port scanning

  -  Security auditing

## Ports:

A port is a virtual gate on a device where network connections start and end.

Ports range from 0 to 65535.

Each port is associated with a specific service (e.g., HTTP, FTP, SSH).

| Port | Service        | Protocol |
| ---- | -------------- | -------- |
| 22   | SSH            | TCP      |
| 80   | HTTP           | TCP      |
| 443  | HTTPS          | TCP      |
| 3389 | Remote Desktop | TCP      |


## OpenPort:

Open ports are actively listening for connections.

They are potential entry points for attackers.

Every open port = a running service = a possible vulnerability

## Types of Port States in Nmap:

open	      :Port is accepting connections
closed	    :Port is accessible but no service is listening
filtered	  :Port is blocked by a firewall or router
unfiltered	:Nmap can’t determine the state

## Commonly Exploited Open Ports:

| Port    | Service | Risk Example                              |
| ------- | ------- | ----------------------------------------- |
| 21      | FTP     | Plaintext login, anonymous access         |
| 22      | SSH     | Brute-force attacks, weak passwords       |
| 23      | Telnet  | Unencrypted, outdated                     |
| 80      | HTTP    | Web exploits, outdated CMSs               |
| 139/445 | SMB     | EternalBlue, ransomware spread (WannaCry) |
| 3306    | MySQL   | Database leakage                          |
| 3389    | RDP     | Remote desktop hijacking                  |

## Security Implications:

  - Properly configured

  -  Updated

  - Access-restricted (firewalled or internal-only)

You should close unused ports or filter them with iptables or ufw.

## Network Range:
- 192.168.1.0/24

## SYN Scan:

A SYN scan sends SYN (synchronize) packets to target ports, just like the first step of a TCP handshake.

   - If a port is open, the target responds with SYN-ACK

   - If closed, the target replies with RST

   - If filtered, there may be no response or ICMP unreachable

🔒 It’s called a "stealth scan" because it doesn’t complete the handshake — so many systems don’t log it as a full connection.



## Command Used:

| Part             | Meaning                             |
| ---------------- | ----------------------------------- |
| `sudo`           | Needed for low-level packet sending |
| `nmap`           | Runs the Nmap tool                  |
| `-sS`            | Tells Nmap to use SYN scan          |
| `192.168.1.0/24` | Scans the entire local subnet       |


```bash
sudo nmap -sS 192.168.1.0/24 -oN scan-results.txt
