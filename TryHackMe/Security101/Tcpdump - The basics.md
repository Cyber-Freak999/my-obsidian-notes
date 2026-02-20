---
tags:
  - network
  - cli
  - tool
  - recon
link: https://tryhackme.com/room/tcpdump
prerequisites:
  - "[[Networking Concepts]]"
  - "[[Networking Core Protocols]]"
  - "[[Networking Essentials]]"
  - "[[Networking Secure Protocols]]"
---
# Basic Packet Capture
The first thing to decide is which network interface to listen to using `-i INTERFACE`. You can choose to listen on all available interfaces using `-i any`; alternatively, you can specify an interface you want to listen on, such as `-i eth0`.
A command such as `ip address show` (or merely `ip a s`) would list the available network interfaces.

| Command                | Explanation                                                       |
| ---------------------- | ----------------------------------------------------------------- |
| `tcpdump -i INTERFACE` | Captures packets on a specific network interface                  |
| `tcpdump -w FILE`      | Writes captured packets to a file                                 |
| `tcpdump -r FILE`      | Reads captured packets from a file                                |
| `tcpdump -c COUNT`     | Captures a specific number of packets                             |
| `tcpdump -n`           | Don’t resolve IP addresses                                        |
| `tcpdump -nn`          | Don’t resolve IP addresses and don’t resolve protocol numbers     |
| `tcpdump -v`           | Verbose display; verbosity can be increased with `-vv` and `-vvv` |
Consider the following examples:
- `tcpdump -i eth0 -c 50 -v` captures and displays 50 packets by listening on the `eth0` interface, which is a wired Ethernet, and displays them verbosely.
- `tcpdump -i wlo1 -w data.pcap` captures packets by listening on the `wlo1` interface (the WiFi interface) and writes the packets to `data.pcap`. It will continue till the user interrupts the capture by pressing CTRL-C.
- `tcpdump -i any -nn` captures packets on all interfaces and displays them on screen without domain name or protocol resolution.

# Filtering Expressions
| Command                                      | Explanation                                                           |
| -------------------------------------------- | --------------------------------------------------------------------- |
| `tcpdump host IP` or `tcpdump host HOSTNAME` | Filters packets by IP address or hostname                             |
| `tcpdump src host IP` or                     | Filters packets by a specific source host                             |
| `tcpdump dst host IP`                        | Filters packets by a specific destination host                        |
| `tcpdump port PORT_NUMBER`                   | Filters packets by port number                                        |
| `tcpdump src port PORT_NUMBER`               | Filters packets by the specified source port number                   |
| `tcpdump dst port PORT_NUMBER`               | Filters packets by the specified destination port number              |
| `tcpdump PROTOCOL`                           | Filters packets by protocol; examples include `ip`, `ip6`, and `icmp` |
Three logical operators that can be handy:
- `and`: Captures packets where both conditions are true. For example, `tcpdump host 1.1.1.1 and tcp` captures `tcp` traffic with `host 1.1.1.1`.
- `or`: Captures packets when either one of the conditions is true. For instance, `tcpdump udp or icmp` captures UDP or ICMP traffic.
- `not`: Captures packets when the condition is not true. For example, `tcpdump not tcp` captures all packets except TCP segments; we expect to find UDP, ICMP, and ARP packets among the results.
# Advanced Filtering
We can limit the displayed packets to those smaller or larger than a certain length:
- `greater LENGTH`: Filters packets that have a length greater than or equal to the specified length
- `less LENGTH`: Filters packets that have a length less than or equal to the specified length
It is recommended you check the `pcap-filter` manual page by issuing the command `man pcap-filter`

Using pcap-filter, Tcpdump allows you to refer to the contents of any byte in the header using the following syntax `proto[expr:size]`, where:
- `proto` refers to the protocol. For example, `arp`, `ether`, `icmp`, `ip`, `ip6`, `tcp`, and `udp` refer to ARP, Ethernet, ICMP, IPv4, IPv6, TCP, and UDP respectively.
- `expr` indicates the byte offset, where `0` refers to the first byte.
- `size` indicates the number of bytes that interest us, which can be one, two, or four. It is optional and is one by default.

To better understand this, consider the following two examples from the pcap-filter manual page:
- `ether[0] & 1 != 0` takes the first byte in the Ethernet header and the decimal number 1 (i.e., `0000 0001` in binary) and applies the `&` (the And binary operation). It will return true if the result is not equal to the number 0 (i.e., `0000 0000`). The purpose of this filter is to show packets sent to a multicast address. A multicast Ethernet address is a particular address that identifies a group of devices intended to receive the same data.  
- `ip[0] & 0xf != 5` takes the first byte in the IP header and compares it with the hexadecimal number F (i.e., `0000 1111` in binary). It will return true if the result is not equal to the (decimal) number 5 (i.e., `0000 0101` in binary). The purpose of this filter is to catch all IP packets with options.

You can use `tcp[tcpflags]` to refer to the TCP flags field. The following TCP flags are available to compare with:

- `tcp-syn` TCP SYN (Synchronize)
- `tcp-ack` TCP ACK (Acknowledge)
- `tcp-fin` TCP FIN (Finish)
- `tcp-rst` TCP RST (Reset)
- `tcp-push` TCP Push

Based on the above, we can write:

- `tcpdump "tcp[tcpflags] == tcp-syn"` to capture TCP packets with **only** the SYN (Synchronize) flag set, while all the other flags are unset.
- `tcpdump "tcp[tcpflags] & tcp-syn != 0"` to capture TCP packets with **at least** the SYN (Synchronize) flag set.
- `tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"` to capture TCP packets with **at least** the SYN (Synchronize) **or** ACK (Acknowledge) flags set.
# Displaying Packets
| Command       | Explanation                                        |
| ------------- | -------------------------------------------------- |
| `tcpdump -q`  | Quick and quite: brief packet information          |
| `tcpdump -e`  | Include MAC addresses                              |
| `tcpdump -A`  | Print packets as ASCII encoding                    |
| `tcpdump -xx` | Display packets in hexadecimal format              |
| `tcpdump -X`  | Show packets in both hexadecimal and ASCII formats |