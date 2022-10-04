
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
crackmapexec smb <IP> --shares

crackmapexec smb <IP> -u '' -p '' --shares

crackmapexec smb <IP> -u '' --shares

crackmapexec smb <IP> --pass-pol

crackmapexec smb --users

smbmap -H <IP>

smbclient -L //<IP>

smbclient --no-pass //<IP>/<share name> -U''
  
  
  
