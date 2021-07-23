# Networking

### IPv4 Addressing/Subnetting
| slash notation | net mask        | number of hosts |
|----------------|-----------------|-----------------|
| /0             | 0.0.0.0         | 4294967296      |
| /1             | 128.0.0.0       | 2147483648      |
| /2             | 192.0.0.0       | 1073741824      |
| /3             | 224.0.0.0       | 536870912       |
| /4             | 240.0.0.0       | 268435456       |
| /5             | 248.0.0.0       | 134217728       |
| /6             | 252.0.0.0       | 67108864        |
| /7             | 254.0.0.0       | 33554432        |
| /8             | 255.0.0.0       | 16777216        |
| /9             | 255.128.0.0     | 8388608         |
| /10            | 255.192.0.0     | 4194304         |
| /11            | 255.224.0.0     | 2097152         |
| /12            | 255.240.0.0     | 1048576         |
| /13            | 255.248.0.0     | 524288          |
| /14            | 255.252.0.0     | 262144          |
| /15            | 255.254.0.0     | 131072          |
| /16            | 255.255.0.0     | 65536           |
| /17            | 255.255.128.0   | 32768           |
| /18            | 255.255.192.0   | 16384           |
| /19            | 255.255.224.0   | 8192            |
| /20            | 255.255.240.0   | 4096            |
| /21            | 255.255.248.0   | 2048            |
| /22            | 255.255.252.0   | 1024            |
| /23            | 255.255.254.0   | 512             |
| /24            | 255.255.255.0   | 256             |
| /25            | 255.255.255.128 | 128             |
| /26            | 255.255.255.192 | 64              |
| /27            | 255.255.255.224 | 32              |
| /28            | 255.255.255.240 | 16              |
| /29            | 255.255.255.248 | 8               |
| /30            | 255.255.255.252 | 4               |
| /31            | 255.255.255.254 | 2               |
| /32            | 255.255.255.255 | 1               |

### Common ports & Protocols
| Port | Protocol | Hint                   |
|------|----------|------------------------|
| 22   | SSH      |                        |
| 25   | SMTP     |                        |
| 110  | POP3     |                        |
| 115  | SFTP     |                        |
| 143  | IMAP     |                        |
| 80   | HTTP     |                        |
| 443  | HTTPS    |                        |
| 23   | TELNET   |                        |
| 21   | FTP      |                        |
| 3389 | RDP      |                        |
| 3306 | MYSQL    |                        |
| 1433 | MS SQL   |                        |
| 137  | NETBIOS  | find work groups       |
| 138  | NETBIOS  | list shares & machines |
| 139  | NETBIOS  | transit data           |
| 53   | DNS      |                        ||

### Routing

To see what your current routing table looks like use the following commands:
- ip route <b>on Linux</b>
- route print <b>on Windows</b>
- netstat -r <b>on OSX</b>

```
# Adding a new route 
ip route add ROUTETO via ROUTEFROM
```

### MAC Address

To discover the MAC address of the network cards installed, you can use:
- ipconfig /all <b>on Windows</b>
- ip addr <b>on Linux</b>
- ifconfig <b>on OSX</b>

### ARP Cache

You can check the ARP cache of your hosts by typing:
- arp -a <b>on Windows</b>
- ip neighbour <b>on Linux</b>
- arp <b>on OSX</b>

### Netstat Command

To check the listening ports and the current (TCP) connections on a host you can use:
- netstat -ano <b>on Windows</b>
- netstat -tunp <b>on Linux</b>
- netstat -p tcp -p udp <b>together with</b></br>
  lsof -n -i4TCP -i4UDP <b>on MacOS</b>


### Wireshark

Wireshark is a network sniffer and protocol analyzer.

Here are some basic capture filters:

| syntax                   | Description                                                                                  |
|--------------------------|----------------------------------------------------------------------------------------------|
| ip                       | Only packets using IP as layer 3 protocol.                                                   |
| not ip                   | The opposite of the previous syntax.                                                         |
| tcp port 80              | Packets where the source or destination TCP port is 80.                                      |
| net 192.168.54.0/24      | Packets from and to the specified network.                                                   |
| src port 1234            | The source port must be 1234; the transport protocol does not matter.                        |
| src net 192.168.1.0/24   | The source IP address must be in the specified network.                                      |
| host 192.168.45.65       | All the packets from or to the specified host.                                               |
| host www.example.com | All the packets from or to the specified hostname.                                           |

