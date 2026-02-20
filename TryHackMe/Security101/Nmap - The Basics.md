---
tags:
  - recon
  - tool
  - cli
  - network
prerequisites:
  - "[[Networking Concepts]]"
  - "[[Networking Essentials]]"
  - "[[Networking Core Protocols]]"
  - "[[Networking Secure Protocols]]"
link: https://tryhackme.com/room/nmap
---
# Host Discovery
- IP range using `-`: If you want to scan all the IP addresses from 192.168.0.1 to 192.168.0.10, you can write `192.168.0.1-10`
- IP subnet using `/`: If you want to scan a subnet, you can express it as `192.168.0.1/24`, and this would be equivalent to `192.168.0.0-255`
- Hostname: You can also specify your target by hostname, for example, `example.thm`

`-sn` aims to discover live hosts without attempting to discover the services running on them. This scan might be helpful if you want to discover the devices on a network without causing much noise. However, this won’t tell us which services are running.
# Port Scanning
By design, TCP has 65,535 ports, and the same applies to UDP.

| Option      | Explanation                                                                                        |
| ----------- | -------------------------------------------------------------------------------------------------- |
| `-sT`       | TCP connect scan – complete three-way handshake                                                    |
| `-sS`       | TCP SYN – only first step of the three-way handshake. It is considered a relatively stealthy scan. |
| `-sU`       | UDP scan                                                                                           |
| `-F`        | Fast mode – scans the 100 most common ports                                                        |
| `-p[range]` | Specifies a range of port numbers – `-p-` scans all the ports                                      |
For example, `-p10-1024` scans from port 10 to port 1024, while `-p-25` will scan all the ports between 1 and 25. Note that `-p-` scans all the ports and is equivalent to `-p1-65535` and is the best option if you want to be as thorough as possible.

Although most services use TCP for communication, many use UDP. Examples include DNS, DHCP, NTP (Network Time Protocol), SNMP (Simple Network Management Protocol), and VoIP (Voice over IP). UDP does not require establishing a connection and tearing it down afterwards. Furthermore, it is very suitable for real-time communication, such as live broadcasts. All these are reasons to consider scanning for and discovering services listening on UDP ports.
# Version Detection
| Option | Explanation                                          |
| ------ | ---------------------------------------------------- |
| `-O`   | OS detection                                         |
| `-sV`  | Service and version detection                        |
| `-A`   | OS detection, version detection, and other additions |
| `-Pn`  | Scan hosts that appear to be down                    |
# Timing
|Option|Explanation|
|---|---|
|`-T<0-5>`|Timing template – paranoid (0), sneaky (1), polite (2), normal (3), aggressive (4), and insane (5)|
|`--min-parallelism <numprobes>` and `--max-parallelism <numprobes>`|Minimum and maximum number of parallel probes|
|`--min-rate <number>` and `--max-rate <number>`|Minimum and maximum rate (packets/second)|
|`--host-timeout`|Maximum amount of time to wait for a target host|
Running your scan at its normal speed might trigger an IDS or other security solutions. It is reasonable to control how fast a scan should go. Nmap gives you six timing templates, and the names say it all: paranoid (0), sneaky (1), polite (2), normal (3), aggressive (4), and insane (5). You can pick the timing template by its name or number. For example, you can add `-T0` (or `-T 0`) or `-T paranoid` to opt for the slowest timing.
# Outputs
The best way to get more updates about what’s happening is to enable verbose output by adding `-v`.
Most likely, the `-v` option is more than enough for verbose output; however, if you are still unsatisfied, you can increase the verbosity level by adding another “v” such as `-vv` or even `-vvvv`. You can also specify the verbosity level directly, for example, `-v2` and `-v4`. You can even increase the verbosity level by pressing “v” after the scan already started.

If all this verbosity does not satisfy your needs, you must consider the `-d` for debugging-level output. Similarly, you can increase the debugging level by adding one or more “d” or by specifying the debugging level directly. The maximum level is `-d9`; before choosing that, make sure you are ready for thousands of information and debugging lines.

You can select the following format for saving your scan report:
- `-oN <filename>` - Normal output
- `-oX <filename>` - XML output
- `-oG <filename>` - `grep`-able output (useful for `grep` and `awk`)
- `-oA <basename>` - Output in all major formats