ping internetlogin.cu.edu.ng to get ip address

did a network scan
```bash
❯ sudo nmap -A 172.16.55.254 -T4 -sV -Pn

Starting Nmap 7.92 ( https://nmap.org ) at 2025-07-13 00:22 WAT
Nmap scan report for 172.16.55.254
Host is up (0.41s latency).
Not shown: 994 filtered tcp ports (no-response)
PORT     STATE  SERVICE      VERSION
22/tcp   open   ssh          (protocol 2.0)
| fingerprint-strings: 
|   NULL: 
|_    SSH-2.0-qPYVp
113/tcp  closed ident
179/tcp  open   tcpwrapped
443/tcp  open   ssl/https?
|_ssl-date: TLS randomness does not represent time
800/tcp  open   mdbs_daemon?
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, Help, Kerberos, RPCCheck, RTSPRequest, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServerCookie, X11Probe: 
|     HTTP/1.1 400 Bad Request
|     Connection: close
|   FourOhFourRequest: 
|     HTTP/1.1 301 Moved Permanently
|     X-Frame-Options: SAMEORIGIN
|     Content-Security-Policy: frame-ancestors 'self'
|     X-XSS-Protection: 1; mode=block
|     Strict-Transport-Security: max-age=0
|     location: https://undefined:4430/nice%20ports%2C/Tri%6Eity.txt%2ebak
|     Date: Sat, 12 Jul 2025 23:23:18 GMT
|     Connection: close
|   GetRequest, HTTPOptions: 
|     HTTP/1.1 301 Moved Permanently
|     X-Frame-Options: SAMEORIGIN
|     Content-Security-Policy: frame-ancestors 'self'
|     X-XSS-Protection: 1; mode=block
|     Strict-Transport-Security: max-age=0
|     location: https://undefined:4430/
|     Date: Sat, 12 Jul 2025 23:23:08 GMT
|_    Connection: close
1000/tcp open   http         FortiGate Application filtering (Auth server 172.16.55.254:1000)
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :

==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port22-TCP:V=7.92%I=7%D=7/13%Time=6872EE54%P=x86_64-redhat-linux-gnu%r(
SF:NULL,F,"SSH-2\.0-qPYVp\r\n");

==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port800-TCP:V=7.92%I=7%D=7/13%Time=6872EE59%P=x86_64-redhat-linux-gnu%r
SF:(GetRequest,112,"HTTP/1\.1\x20301\x20Moved\x20Permanently\r\nX-Frame-Op
SF:tions:\x20SAMEORIGIN\r\nContent-Security-Policy:\x20frame-ancestors\x20
SF:'self'\r\nX-XSS-Protection:\x201;\x20mode=block\r\nStrict-Transport-Sec
SF:urity:\x20max-age=0\r\nlocation:\x20https://undefined:4430/\r\nDate:\x2
SF:0Sat,\x2012\x20Jul\x202025\x2023:23:08\x20GMT\r\nConnection:\x20close\r
SF:\n\r\n")%r(HTTPOptions,112,"HTTP/1\.1\x20301\x20Moved\x20Permanently\r\
SF:nX-Frame-Options:\x20SAMEORIGIN\r\nContent-Security-Policy:\x20frame-an
SF:cestors\x20'self'\r\nX-XSS-Protection:\x201;\x20mode=block\r\nStrict-Tr
SF:ansport-Security:\x20max-age=0\r\nlocation:\x20https://undefined:4430/\
SF:r\nDate:\x20Sat,\x2012\x20Jul\x202025\x2023:23:08\x20GMT\r\nConnection:
SF:\x20close\r\n\r\n")%r(RTSPRequest,2F,"HTTP/1\.1\x20400\x20Bad\x20Reques
SF:t\r\nConnection:\x20close\r\n\r\n")%r(RPCCheck,2F,"HTTP/1\.1\x20400\x20
SF:Bad\x20Request\r\nConnection:\x20close\r\n\r\n")%r(DNSVersionBindReqTCP
SF:,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConnection:\x20close\r\n\r\n
SF:")%r(DNSStatusRequestTCP,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConn
SF:ection:\x20close\r\n\r\n")%r(Help,2F,"HTTP/1\.1\x20400\x20Bad\x20Reques
SF:t\r\nConnection:\x20close\r\n\r\n")%r(SSLSessionReq,2F,"HTTP/1\.1\x2040
SF:0\x20Bad\x20Request\r\nConnection:\x20close\r\n\r\n")%r(TerminalServerC
SF:ookie,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConnection:\x20close\r\
SF:n\r\n")%r(TLSSessionReq,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConne
SF:ction:\x20close\r\n\r\n")%r(Kerberos,2F,"HTTP/1\.1\x20400\x20Bad\x20Req
SF:uest\r\nConnection:\x20close\r\n\r\n")%r(SMBProgNeg,2F,"HTTP/1\.1\x2040
SF:0\x20Bad\x20Request\r\nConnection:\x20close\r\n\r\n")%r(X11Probe,2F,"HT
SF:TP/1\.1\x20400\x20Bad\x20Request\r\nConnection:\x20close\r\n\r\n")%r(Fo
SF:urOhFourRequest,135,"HTTP/1\.1\x20301\x20Moved\x20Permanently\r\nX-Fram
SF:e-Options:\x20SAMEORIGIN\r\nContent-Security-Policy:\x20frame-ancestors
SF:\x20'self'\r\nX-XSS-Protection:\x201;\x20mode=block\r\nStrict-Transport
SF:-Security:\x20max-age=0\r\nlocation:\x20https://undefined:4430/nice%20p
SF:orts%2C/Tri%6Eity\.txt%2ebak\r\nDate:\x20Sat,\x2012\x20Jul\x202025\x202
SF:3:23:18\x20GMT\r\nConnection:\x20close\r\n\r\n");

Aggressive OS guesses: 
Fortinet FortiGate 100D firewall (89%), Vonage V-Portal VoIP adapter (89%), Sun OpenSolaris 2009.06 (88%), Sun Solaris 8 (SPARC) (88%), Sun Solaris 9 (88%), Microsoft Windows Phone 7.5 or 8.0 (88%), Microsoft Windows Server 2012 R2 (87%), Microsoft Windows Vista Home Premium SP1 (87%), Microsoft Windows Embedded Standard 7 (86%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 15 hops

TRACEROUTE (using port 113/tcp)
HOP RTT        ADDRESS
1   ... 14
15  1218.02 ms 172.16.55.254

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 325.69 seconds
```

from the os scan, it shows that the school is using a fortinet fortigate 100d firewall.

---

Port 800 redirects to port 4430(https://172.16.55.254:4430/login) 
this is from my scan(https://172.16.55.254:4430/login?redir=%2Fnice%2520ports%252C%2FTri%256Eity.txt%252ebak) 

```bash
❯ curl -k -i https://172.16.55.254:4430/nice%20ports%2C/Tri%6Eity.txt%2ebak
HTTP/2 200 
content-encoding: gzip
content-type: text/html
etag: f174d96ceb993053c9d2529d5173a441
x-frame-options: SAMEORIGIN
content-security-policy: frame-ancestors 'self'
x-xss-protection: 1; mode=block
strict-transport-security: max-age=15552000
date: Sun, 13 Jul 2025 01:19:16 GMT
```

both urls land in the same place(the .bak file is not there for some reason, most likely a misconfig)
4430 is a login page(fortinet related cuz of the favicon i am seeing)
![[Pasted image 20250714004242.png]]

the login page has a sign option with security fabric.
Inspecting the page source reveals this url => 'https://165.73.200.254:4430/saml/login/'

Clicking the security fabric redirects to a moodle looking login page(https://sso.cu.edu.ng:8443/auth/realms/Cu/protocol/saml?SAMLRequest=fZLLTsMwEEV%2FJfK%2BseMkDVhtUWmoqMQjooUFG2SSKVhK7OKxefw9TspzATtrPEe%2B58oTlF27E3PvHvUVPHlAF712rUYxXEyJt1oYiQqFlh2gcLVYz8%2FPBI%2BZ2FnjTG1a8gP5n5CIYJ0ymkSrckruxmV%2BfJidHKbzcVaUi7zgy5Lzk%2FGSFYwneU6iG7AY9qck4AFC9LDS6KR2YcR4PmLFKEk3PBVZIlJ2S6IyOCgt3UA9OrdDQSmiiWsfQ%2BNj%2FSAOsiylMjhTC7LtkC48%2FZShvQWJlsbWMNQyJVvZIvSPVyG%2FeoavSfXBHCvdKP3wv%2Fv9fgnF6WZTjarL9YZE888%2BFkaj78CuwT6rGq6vzr6zJ%2BM8LtKYMxbzPBMhOxtC0iNZI5lN%2BrMYmrGznvkD6cDJRjpJJ%2FQnMdn%2FgIuQd1VWplX1Wy%2FfSfe3ThInw0Q1o%2B2wKrzGHdRqq6AJVm1rXhahWheqctYDobP9o79%2F2uwd&RelayState=%2F&fallback=https%3A%2F%2F172.16.55.254%3A4430%2Flogin)
![[Pasted image 20250714004226.png]]
I noticed that my moodle creds could login into the platform. Problem is my account does not have permission levels required to be on that site.
![[Pasted image 20250714004328.png]]
*Will try to research SAML assertion attributes and see if i can edit my request to have it.*

![[Pasted image 20250714010705.png]]
Headers of the request
![[Pasted image 20250714010731.png]]
Request body(notice the `credentialId`)

Clicking on either `Login Locally` or `switch account` will redirect to this url(https://165.73.200.254:4430/login)
![[Pasted image 20250714010922.png]]
still looks like our initial ip login page. the security fabric button redirects back to the same page.


---
Here is my finding from when i tried logging in on the fortigate page

Request
```http
POST /logincheck HTTP/2
Host: 172.16.55.254:4430
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Pragma: no-cache
Cache-Control: no-store, no-cache, must-revalidate
If-Modified-Since: Sat, 1 Jan 2000 00:00:00 GMT
Content-Type: text/plain;charset=UTF-8
Content-Length: 51
Origin: https://172.16.55.254:4430
Sec-Gpc: 1
Referer: https://172.16.55.254:4430/login?redir=%2F
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Priority: u=0
Te: trailers

ajax=1&username=oracle&secretkey=password&redir=%2F
```

Response
```http
HTTP/2 200 OK
Date: Sun, 13 Jul 2025 00:45:17 GMT
X-Frame-Options: SAMEORIGIN
Content-Security-Policy: frame-ancestors 'self'
X-Xss-Protection: 1; mode=block
Content-Length: 1
Content-Type: text/html

0
```


Upon asking gpt, they said that if the response is `1` then it is successful and that `0` means failed attempt

tried bruteforcing the credentials via burpsuite but to no avail. I later realize it was a bad idea as the response size is the same(210) whether it was successful or not.

---

I tried a recommendation from gpt

```bash
❯ openssl s_client -connect 172.16.55.254:4430 -servername 172.16.55.254
Connecting to 172.16.55.254
CONNECTED(00000003)
depth=2 C=US, ST=New Jersey, L=Jersey City, O=The USERTRUST Network, CN=USERTrust RSA Certification Authority
verify return:1
depth=1 C=GB, ST=Greater Manchester, L=Salford, O=Sectigo Limited, CN=Sectigo RSA Domain Validation Secure Server CA
verify return:1
depth=0 CN=*.cu.edu.ng
verify error:num=10:certificate has expired
notAfter=Jan 26 23:59:59 2022 GMT
verify return:1
depth=0 CN=*.cu.edu.ng
notAfter=Jan 26 23:59:59 2022 GMT
verify return:1
---
Certificate chain
 0 s:CN=*.cu.edu.ng
   i:C=GB, ST=Greater Manchester, L=Salford, O=Sectigo Limited, CN=Sectigo RSA Domain Validation Secure Server CA
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA256
   v:NotBefore: Dec 26 00:00:00 2020 GMT; NotAfter: Jan 26 23:59:59 2022 GMT
 1 s:C=GB, ST=Greater Manchester, L=Salford, O=Sectigo Limited, CN=Sectigo RSA Domain Validation Secure Server CA
   i:C=US, ST=New Jersey, L=Jersey City, O=The USERTRUST Network, CN=USERTrust RSA Certification Authority
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA384
   v:NotBefore: Nov  2 00:00:00 2018 GMT; NotAfter: Dec 31 23:59:59 2030 GMT
 2 s:C=US, ST=New Jersey, L=Jersey City, O=The USERTRUST Network, CN=USERTrust RSA Certification Authority
   i:C=GB, ST=Greater Manchester, L=Salford, O=Comodo CA Limited, CN=AAA Certificate Services
   a:PKEY: rsaEncryption, 4096 (bit); sigalg: RSA-SHA384
   v:NotBefore: Mar 12 00:00:00 2019 GMT; NotAfter: Dec 31 23:59:59 2028 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFsDCCBJigAwIBAgIRAORY8nySWL87QjzqbHqIbPQwDQYJKoZIhvcNAQELBQAw
gY8xCzAJBgNVBAYTAkdCMRswGQYDVQQIExJHcmVhdGVyIE1hbmNoZXN0ZXIxEDAO
BgNVBAcTB1NhbGZvcmQxGDAWBgNVBAoTD1NlY3RpZ28gTGltaXRlZDE3MDUGA1UE
AxMuU2VjdGlnbyBSU0EgRG9tYWluIFZhbGlkYXRpb24gU2VjdXJlIFNlcnZlciBD
QTAeFw0yMDEyMjYwMDAwMDBaFw0yMjAxMjYyMzU5NTlaMBYxFDASBgNVBAMMCyou
Y3UuZWR1Lm5nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA9tU2XCbX
xGM0kwmQMRi3+o6MbkXAckh4Af9csGbk2HOotzqyinWs3c2MFDY0XAHP8CaYOf5E
hA+fXebNL36nK3M0ITeCpjqi3sbE6536s2GPFXBkvEmkrb4+n0/RVzKEiElHKGOF
ndrnh4zUhVGWO+nNF7250vOQIZRMfoH8GVw26P7lqX/4iN/lf1rigsJZJzMXzHZR
8SVJiLfYoRl0d7dhp/7Xw101GlAqtxYPrfDwPCGQ2AOTYkdlymHN0g91LCS9Y/kZ
zEW2iv9G6JtWPPf6KvFcq8J+iCqOjnK7RqMX6hgGlfhTtEfADLlwyyKkHm5AWU8N
XdttOhxr1yVKQQIDAQABo4ICfTCCAnkwHwYDVR0jBBgwFoAUjYxexFStiuF36Zv5
mwXhuAGNYeEwHQYDVR0OBBYEFMy6wUogJC+nlTnbST8Tu4QpNx6LMA4GA1UdDwEB
/wQEAwIFoDAMBgNVHRMBAf8EAjAAMB0GA1UdJQQWMBQGCCsGAQUFBwMBBggrBgEF
BQcDAjBJBgNVHSAEQjBAMDQGCysGAQQBsjEBAgIHMCUwIwYIKwYBBQUHAgEWF2h0
dHBzOi8vc2VjdGlnby5jb20vQ1BTMAgGBmeBDAECATCBhAYIKwYBBQUHAQEEeDB2
ME8GCCsGAQUFBzAChkNodHRwOi8vY3J0LnNlY3RpZ28uY29tL1NlY3RpZ29SU0FE
b21haW5WYWxpZGF0aW9uU2VjdXJlU2VydmVyQ0EuY3J0MCMGCCsGAQUFBzABhhdo
dHRwOi8vb2NzcC5zZWN0aWdvLmNvbTAhBgNVHREEGjAYggsqLmN1LmVkdS5uZ4IJ
Y3UuZWR1Lm5nMIIBAwYKKwYBBAHWeQIEAgSB9ASB8QDvAHUARqVV63X6kSAwtaKJ
afTzfREsQXS+/Um4havy/HD+bUcAAAF2noZnRgAABAMARjBEAiAXbslJe6MRgps6
t6bjMX2Kwfy19D4IVg+U2+uKR2oBIwIgL0wyuU5uzcaIMDpBfX6r/8U8sGLTfOZu
d96yD2CvD7YAdgDfpV6raIJPH2yt7rhfTj5a6s2iEqRqXo47EsAgRFwqcwAAAXae
hmfQAAAEAwBHMEUCIBcPI3wuLaa9mkio681kHZzI+2C15LUg0zvvdRsVI+ZzAiEA
pxpB7Vtr4TqNJsXo9kFhrpO/hAoSdVHlB1/ZikLvALowDQYJKoZIhvcNAQELBQAD
ggEBAGq18bp3p9PPHQFxu2OM1/UWStCOEb7VrRF1gttKfLw+11pFOPIf4SP7pWh5
Gb3up9cOK85ZtI872P6JAXcWzCjRnS+RBR8z8bKwsciZujJJQxL4YmG2kxN5KhsC
/IUsVAROsRH0rsbQ+b5Uvwx6D15D9vyHoYAHQy7M2N2nIcnPqGq36cEwmKWq/t63
bfDrMdSSjDTNuvBkgLQ+H+hL+8VAAM7XkzKebVLPPSpRb3yEyOCbVnQ1GrC5uUdF
KHNnEDBA1jQxpSkTzCUx7gH19mVkfWxjc2akaIazmrPuATp7eoKrO2lWN1QeDZBI
HMc2QGJleTdQVugIA+7CQ5ddZbs=
-----END CERTIFICATE-----
subject=CN=*.cu.edu.ng
issuer=C=GB, ST=Greater Manchester, L=Salford, O=Sectigo Limited, CN=Sectigo RSA Domain Validation Secure Server CA
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 4998 bytes and written 404 bytes
Verification error: certificate has expired
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 2048 bit
This TLS version forbids renegotiation.
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 10 (certificate has expired)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: FD18AEA6F82EDEE748C2CE9128CDC4B1121C503423EE41CE6D2BE464E944AECB
    Session-ID-ctx: 
    Resumption PSK: F8F536E78589EB4D6CCE4D135E5DBFF4AA3719B75D0B0A8EC82C4FE8DC34684FF78DBD7838F6BD42D7C5DE15D890A6AB
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - f3 9d a5 e4 e7 9c 9a 30-f2 ff 7f 3b 63 c8 04 5e   .......0...;c..^
    0010 - 2f 2d 5d 22 72 74 a3 78-13 9d 3e f3 f4 42 54 4e   /-]"rt.x..>..BTN
    0020 - 92 d2 8a 8a 2c bd 86 60-25 46 96 ba 0f b2 56 cf   ....,..`%F....V.
    0030 - 26 63 df 28 94 2a 4a 88-cc 18 2d a9 96 8f fa 1e   &c.(.*J...-.....
    0040 - c9 11 eb d4 a9 96 95 e8-68 74 51 38 88 49 f9 e5   ........htQ8.I..
    0050 - 55 9a a9 3f f0 26 4c 26-63 67 f8 61 2c f0 3f e9   U..?.&L&cg.a,.?.
    0060 - a2 30 86 06 8d 85 c9 e6-7b 0c fc 3f c9 4d 98 c0   .0......{..?.M..
    0070 - 8f 0b 35 97 52 c3 2b 6f-91 42 6b 38 3c b6 8d 17   ..5.R.+o.Bk8<...
    0080 - 73 16 b0 59 f5 d5 4f 87-5d a7 99 0d bd b0 94 59   s..Y..O.]......Y
    0090 - ec 02 eb fd 6f ab 23 7c-24 a9 7d f2 e7 d0 ed 01   ....o.#|$.}.....
    00a0 - 86 f8 6a f3 13 5e 8c a8-c0 cf b9 4a b7 f3 e6 fb   ..j..^.....J....
    00b0 - 93 39 39 67 8a 88 1e 17-57 ed c1 6d 61 e0 3b ee   .99g....W..ma.;.
    00c0 - fa 9c d6 1c 9e 22 28 88-09 61 f0 00 f9 25 01 fa   ....."(..a...%..
    00d0 - 27 93 be 59 3c 45 96 d3-1a b4 cc c1 5a 74 fa b9   '..Y<E......Zt..

    Start Time: 1752364456
    Timeout   : 7200 (sec)
    Verify return code: 10 (certificate has expired)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: D77975289D42BF4E9C4BAD07361C9F9E40D5F79E8F42AE4B3C3E6A3B0D64D500
    Session-ID-ctx: 
    Resumption PSK: 284FD3873B95495A59C03AC72D5DC0F7C80946EB82AF8D33BC30A5893E6C9599E250CEFA05DDF164785012907E61C988
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - f3 9d a5 e4 e7 9c 9a 30-f2 ff 7f 3b 63 c8 04 5e   .......0...;c..^
    0010 - 0d 07 b5 78 24 50 74 0a-cf d0 7b 2d 19 85 6b c5   ...x$Pt...{-..k.
    0020 - 55 26 5e 7c 87 7a 6a 5f-13 65 0e 25 39 42 91 4b   U&^|.zj_.e.%9B.K
    0030 - fa 41 5e 67 eb cb 5e 06-83 2d 15 c6 98 a7 59 87   .A^g..^..-....Y.
    0040 - bb 8c 58 87 45 92 a5 0a-6c 93 84 fd b6 5a 58 1e   ..X.E...l....ZX.
    0050 - bc 2c b5 98 22 92 03 46-59 22 0f df 66 87 63 b8   .,.."..FY"..f.c.
    0060 - d6 e7 14 ea 6e b3 c9 02-59 1d a0 e7 d4 20 66 4e   ....n...Y.... fN
    0070 - 7c 23 18 1c 9e c3 8b f8-70 09 6e ff a5 48 ef e2   |#......p.n..H..
    0080 - 43 36 8f 56 54 4a f1 b6-fe ae 55 94 e9 fb 7b 97   C6.VTJ....U...{.
    0090 - 1f a5 b5 a2 f2 bd 77 61-e2 a4 95 eb 7a 1f ad 53   ......wa....z..S
    00a0 - e8 b2 eb 90 c3 92 4d f9-36 a4 9b db 1c 5b c7 01   ......M.6....[..
    00b0 - 2b a3 1f dc db fb 83 ca-65 9b c5 28 43 6b 0d f0   +.......e..(Ck..
    00c0 - 14 7c de 6e 88 d6 38 a1-b5 f3 cb 4d 66 3a 7d 12   .|.n..8....Mf:}.
    00d0 - 5d 5e 2d 28 ab 71 21 7e-d2 87 f4 84 dd 4c bd 63   ]^-(.q!~.....L.c

    Start Time: 1752364456
    Timeout   : 7200 (sec)
    Verify return code: 10 (certificate has expired)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
80628B10867F0000:error:0A000126:SSL routines::unexpected eof while reading:ssl/record/rec_layer_s3.c:689:
```

From this, we can observe the certificate expired on January 26, 2022. i have nothing to work with here.