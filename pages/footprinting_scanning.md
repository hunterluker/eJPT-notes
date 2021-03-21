# Footprinting & Scanning

This is the infrastrucutre part of the information gathering.

### Mapping a network

Mapping a network helps the pentester get an idea of how the network is structured.

### Ping sweep

Ping sweeping helps find all live hosts in a network range.

```
fping -a -g 192.168.1.0/24 2>/dev/null
nmap -sn 192.168.1.0/24
```

### OS fingerprinting

OS fingerprinting is the process of determinig the operating system used by a host on a network.

```
# OS Detection, no ping
nmap -Pn -O <target(s)>
```

### Port Scanning

Port scanning allows for discvoery of running daemons and services of each node on the network.

```
# TCP SYN scan or stealth scan
nmap -Ss <target>

# Scripts and version detection
nmap -sC -sV <target>

# All ports, scripts, version
nmap -sC -sV -p- <target>

# UDP and Version check
nmap -sU -sV <target>

# Most used scan
# OS, version, scripts, traceroute, and all ports
nmap -A -p- <target>
```
