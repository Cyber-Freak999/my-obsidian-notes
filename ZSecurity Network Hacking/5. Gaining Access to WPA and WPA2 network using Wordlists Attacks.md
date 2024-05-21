# Saving Cracking Session
default cracking
`aircrack-ng <handshake-file> -w <wordlist-file>`

using johntheripper 
take the wordlist print it out and pipe it into aircrack
`john --wordlist=<path-to-wordlsit> --stdout --session=<name-of-your-choice>| aircrack-ng -w - -b <access-point-mac-address> <handshake-file>`

# Restoring the session
`john --restore=<session-name> | aircrack-ng -w - -b <access-point-mac-address> <handshake-file>`

# Generate wordlists and passing it to Aircrack-ng
`crunch <minimum-number-of-character> <maximum-number-of-character> <characters-to-be-used> -o <file-to-save-to>`

8 is the minimum length of character for passwords

By not specifying the characters to be used, crunch will used all possible characters. This generates very large files. 
You can pipe this to aircrack-ng

`crunch <minimum-number-of-character> <maximum-number-of-character> <characters-to-be-used> | aircrack-ng -w - -b <access-point-mac-address> <handshake-file>`

# Generate wordlist and pipe it to Aircrack-ng with Pause and Resume Support
## Starting a new session
 `crunch 8 8 | john --stdin --session=<session-name> --stdout | aircrack-ng -w - -b <access-point-mac-address> <handshake-file>`
## Restoring a session
`crunch 8 8 | john --restore=<session-name> | aircrack-ng -w - -b <access-point-mac-address> <handshake-file>`

# Using the GPU
Use Hashcat