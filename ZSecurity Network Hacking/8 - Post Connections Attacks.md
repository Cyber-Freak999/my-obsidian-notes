 # Overview
- Capture data
- Bypass HTTPS
- DNS Spoofing
- ARP spoofing
- Bypass router-side security features
- Analyse data flows
- Build your own MITM attacks

# Ettercap
`leafpad /etc/ettercap/etter.conf` => Modify the file to use IP tables and set UIDs to 0

For ARP Spoofing*
`ettercap -Tq -M arp:remote -i <interface-name> /<default-gateway>// /<target-ip-address>//`

## Plugins in Ettercap
- autoadd: auto-add new clients**
- repoison_arp: re-pioson clients after arp broadcasts**
- dns_spoof: dns spoof targets**

`ettercap -Tq -M arp:remote -i <interface-name> -5 ///`