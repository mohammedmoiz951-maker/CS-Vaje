# Lab01 – Introduction to Kali Linux

**Course:** MSc Cybersecurity  
**Environment:** Kali Linux Rolling running in Oracle VirtualBox

## 1. Terminal History (Commands and Outputs)

This document records the commands and terminal outputs provided from the lab. Outputs are transcribed from the user's terminal; no output has been invented. 

```text
┌──(kali㉿kali)-[~]
└─$ whoami                                                                                                                              
kali
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ hostnamectl                                                                   
 Static hostname: kali
       Icon name: computer-vm
         Chassis: vm 💽
      Machine ID: d3ab02d2e96b4806ad45511cf7593a25
         Boot ID: 2594b95ec5d8440c8c9c7b2a4a2bcf43
  Virtualization: oracle
Operating System: Kali GNU/Linux Rolling   
          Kernel: Linux 7.1.5+kali-amd64
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Hardware Version: 1.2
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 19y 11month 3d                  
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ uname -a
Linux kali 7.1.5+kali-amd64 #1 SMP PREEMPT_DYNAMIC Kali 7.1.5-1kali1 (2026-07-29) x86_64 GNU/Linux
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ df -h    
Filesystem      Size  Used Avail Use% Mounted on
udev            934M     0  934M   0% /dev
tmpfs           197M  992K  196M   1% /run
/dev/sda1        79G   39G   37G  52% /
tmpfs           985M  4.0K  985M   1% /dev/shm
none            1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs           985M  8.0K  985M   1% /tmp
Downloads       280G  257G   24G  92% /media/sf_Downloads
none            1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
tmpfs           197M  100K  197M   1% /run/user/1000
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ ip a    
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a3:a0:09 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.101/24 brd 192.168.56.255 scope global dynamic noprefixroute eth0
       valid_lft 503sec preferred_lft 503sec
    inet6 fe80::9903:bcc4:1864:4f90/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:66:a9:80 brd ff:ff:ff:ff:ff:ff
    inet 10.0.3.15/24 brd 10.0.3.255 scope global dynamic noprefixroute eth1
       valid_lft 86301sec preferred_lft 86301sec
    inet6 fe80::63db:1c19:4630:bc80/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ which nmap
/usr/bin/nmap
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ which john
/usr/sbin/john
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ cd /                 
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[/]
└─$ ls -la
total 1048652
drwxr-xr-x  18 root root       4096 Oct 17 14:11 .
drwxr-xr-x  18 root root       4096 Oct 17 14:11 ..
lrwxrwxrwx   1 root root          7 Feb 25  2024 bin -> usr/bin
drwxr-xr-x   3 root root       4096 Oct 17 14:13 boot
drwxr-xr-x  18 root root       3240 Nov  4 02:25 dev
drwxr-xr-x 196 root root      12288 Nov  4 02:25 etc
drwxr-xr-x   3 root root       4096 Feb 25  2024 home
lrwxrwxrwx   1 root root         32 Oct 17 14:11 initrd.img -> boot/initrd.img-7.1.5+kali-amd64
lrwxrwxrwx   1 root root         27 Feb 25  2024 initrd.img.old -> boot/initrd.img-6.6.9-amd64
lrwxrwxrwx   1 root root          7 Feb 25  2024 lib -> usr/lib
lrwxrwxrwx   1 root root          9 Oct 17 13:40 lib32 -> usr/lib32
lrwxrwxrwx   1 root root          9 Feb 25  2024 lib64 -> usr/lib64
drwx------   2 root root      16384 Feb 25  2024 lost+found
drwxr-xr-x   3 root root       4096 Nov  3 02:24 media
drwxr-xr-x   2 root root       4096 Feb 25  2024 mnt
drwxr-xr-x   4 root root       4096 Jun  4  2024 opt
dr-xr-xr-x 190 root root          0 Nov  4 02:25 proc
drwx------  13 root root       4096 Nov  4 02:25 root
drwxr-xr-x  40 root root        960 Nov  4 02:26 run
lrwxrwxrwx   1 root root          8 Feb 25  2024 sbin -> usr/sbin
drwxr-xr-x   3 root root       4096 Feb 25  2024 srv
-rw-------   1 root root 1073741824 Feb 25  2024 swapfile
dr-xr-xr-x  13 root root          0 Nov  4 02:25 sys
drwxrwxrwt  12 root root        300 Nov  4 02:27 tmp
drwxr-xr-x  15 root root       4096 Oct 17 13:55 usr
drwxr-xr-x  12 root root       4096 Oct 17 14:37 var
lrwxrwxrwx   1 root root         29 Oct 17 14:11 vmlinuz -> boot/vmlinuz-7.1.5+kali-amd64
lrwxrwxrwx   1 root root         24 Feb 25  2024 vmlinuz.old -> boot/vmlinuz-6.6.9-amd64
                                                                           
┌──(kali㉿kali)-[/]
└─$ cd  
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ wget https://gist.githubusercontent.com/EdwardRayl/3436572afde8ce9e3faf5b7b95356a49/raw/6b25895fce480713560829dec31ac8220ffe5272/gists.txt
--2026-11-04 02:30:39--  https://gist.githubusercontent.com/EdwardRayl/3436572afde8ce9e3faf5b7b95356a49/raw/6b25895fce480713560829dec31ac8220ffe5272/gists.txt
Resolving gist.githubusercontent.com (gist.githubusercontent.com)... 185.199.111.133, 185.199.109.133, 185.199.110.133, ...
Connecting to gist.githubusercontent.com (gist.githubusercontent.com)|185.199.111.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 9634 (9.4K) [text/plain]
Saving to: ‘gists.txt’

gists.txt                                                  100%[======================================================================================================================================>]   9.41K  --.-KB/s    in 0s      

2026-11-04 02:30:39 (74.6 MB/s) - ‘gists.txt’ saved [9634/9634]

                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ ls -l gists.txt
-rw-rw-r-- 1 kali kali 9634 Nov  4 02:30 gists.txt
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ cat gists.txt
Classic Lorem Ipsum Filler Text:
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
Fusce ac turpis quis ligula lacinia aliquet. Mauris ipsum. Nulla metus metus, ullamcorper vel, tincidunt sed, euismod in, nibh. Quisque volutpat condimentum velit. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Nam nec ante. 
Vestibulum sapien. Proin quam. Etiam ultrices. Suspendisse in justo eu magna luctus suscipit. Sed lectus. Integer euismod lacus luctus magna.  Integer id quam. Morbi mi. Quisque nisl felis, venenatis tristique, dignissim in, ultrices sit amet, augue. Proin sodales libero eget ante.


Yar Pirate Ipsum
Bounty belaying pin quarterdeck scuttle grog blossom red ensign hands pillage coxswain heave down. Pressgang long clothes walk the plank pirate driver parley heave down bilge execution dock overhaul. Crack Jennys tea cup scallywag Pirate Round rutters belay bowsprit bring a spring upon her cable Brethren of the Coast clap of thunder Jack Tar.
Furl Buccaneer blow the man down take a caulk tender tackle booty lateen sail killick gangway. Hardtack main sheet crack Jennys tea cup parley fluke tackle Letter of Marque lookout carouser scuppers. Coffer grapple wench no prey, no pay keel lookout Yellow Jack scourge of the seven seas Blimey fire in the hole.
Splice the main brace heave down hulk provost killick Letter of Marque bilge rat flogging grog blossom Chain Shot. Warp to go on account gaff scallywag line man-of-war hands crack Jennys tea cup weigh anchor Sink me. Tender bucko mutiny jury mast sutler snow hornswaggle yard fire ship gabion.


Pompy Ipsum
Pommy ipsum 'tis you 'avin a laugh that's ace complete mare roast beef pulled out the eating irons, two weeks on't trot farewell gravy cheese and chips jellied eels middle class River Song, jammy git make a brew fish and chips one feels that golly bloke. Bottled it gosh up the duff bow ties are cool queer as a clockwork orange, jellied eels bit of a Jack the lad doolally Northeners get away with ya, well fit completely starkers treacle. Bad Wolf not some sort of dosshouse corgi tad doofer fork out working class, blighty pork scratchings every fortnight rambunctious bow ties are cool.
Marvelous rivetting stuff bent as a nine bob note taking the mick owt terribly Sonic Screwdriver, it's me peepers a bit wonky jolly hockey sticks the fuzz on his bill. Cor blimey' naff one would like curry sauce lost her marbles bloody shambles down South what a load of cobblers because there was nothing on the gogglebox see a man about a dog, bangers and mash easy peasy yorkshire mixture bog off goggledegook chinwag nuthouse cornish pasty. Ey up pigeons in Trafalgar Square clotted cream on the beat posh nosh real ale come hither man and his whippet jolly, oo ecky thump I'd reet fancy a you mean it ain't me noggin' bog off and thus tosser what a load of cobblers.
Biscuits numpty trouble and strife absolute know your onions ridicule grab a jumper, well chuffed twiglets pie-eyed twiglets squirrel. Know your onions guinness Big Ben scally I'm off to Bedfordshire fork out, snotty nosed brat and thus eton mess. Kate and Will scones one would like the old bill hadn't done it in donkey's years, have a gander Shakespeare indeed horses for courses lost her marbles, throw a paddy therewith bread and butter pudding. Manky houlligan Dr. Watson clock round the earhole crumpets The Hounds of Baskerville gobsmacked golly, well fit corgi knackered willy bent as a nine bob note ee bah gum cor blimey', devonshire cream tea off t'shop teacakes daft cow a cuppa make a brew.
I could reet fancy a real ale pikey, round our gaff.


DeLorean Ipsum
Silence Earthling. my name is Darth Vader. I'm am an extra-terrestrial from the planet Vulcan. No no no no no, Marty, both you and Jennifer turn out fine. It's your kids, Marty, something has got to be done about your kids. Great Scott. Let me see that photograph again of your brother. Just as I thought, this proves my theory, look at your brother. Well gee, I don't know. Marty, such a nice name.
Hey Marty, I'm not your answering service, but you're outside pouting about the car, Jennifer Parker called you twice. Say that again. Calvin, why do you keep calling me Calvin? Marty, you didn't fall asleep, did you? I'm too loud. I can't believe it. I'm never gonna get a chance to play in front of anybody.
Alright, okay listen, keep your pants on, she's over in the cafe. God, how do you do this? What made you change your mind, George? Yeah I know, If you put your mind to it you could accomplish anything. That Biff, what a character. Always trying to get away with something. Been on top of Biff ever since high school. Although, if it wasn't for him- I noticed you band is on the roster for dance auditions after school today. Why even bother Mcfly, you haven't got a chance, you're too much like your own man. No McFly ever amounted to anything in the history of Hill Valley. It was meant to be. Anyway, if Grandpa hadn't hit him, then none of you would have been born.


Fillerati Text (Herman Melville, H.G. Wells, etc)
I could not help it, but I began to feel suspicious of this "dark complexioned" harpooneer. At any rate, I made up my mind that if it so turned out that we should sleep together, he must undress and get into bed before I did.
Supper over, the company went back to the bar-room, when, knowing not what else to do with myself, I resolved to spend the rest of the evening as a looker on.
Presently a rioting noise was heard without. Starting up, the landlord cried, "That's the Grampus's crew. I seed her reported in the offing this morning; a three years' voyage, and a full ship. Hurrah, boys; now we'll have the latest news from the Feegees."
A tramping of sea boots was heard in the entry; the door was flung open, and in rolled a wild set of mariners enough. Enveloped in their shaggy watch coats, and with their heads muffled in woollen comforters, all bedarned and ragged, and their beards stiff with icicles, they seemed an eruption of bears from Labrador. They had just landed from their boat, and this was the first house they entered. No wonder, then, that they made a straight wake for the whale's mouth—the bar—when the wrinkled little old Jonah, there officiating, soon poured them out brimmers all round. One complained of a bad cold in his head, upon which Jonah mixed him a pitch-like potion of gin and molasses, which he swore was a sovereign cure for all colds and catarrhs whatsoever, never mind of how long standing, or whether caught off the coast of Labrador, or on the weather side of an ice-island.
The liquor soon mounted into their heads, as it generally does even with the arrantest topers newly landed from sea, and they began capering about most obstreperously.
I observed, however, that one of them held somewhat aloof, and though he seemed desirous not to spoil the hilarity of his shipmates by his own sober face, yet upon the whole he refrained from making as much noise as the rest. This man interested me at once; and since the sea-gods had ordained that he should soon become my shipmate (though but a sleeping-partner one, so far as this narrative is concerned), I will here venture upon a little description of him. He stood full six feet in height, with noble shoulders, and a chest like a coffer-dam. I have seldom seen such brawn in a man. His face was deeply brown and burnt, making his white teeth dazzling by the contrast; while in the deep shadows of his eyes floated some reminiscences that did not seem to give him much joy. His voice at once announced that he was a Southerner, and from his fine stature, I thought he must be one of those tall mountaineers from the Alleghanian Ridge in Virginia. When the revelry of his companions had mounted to its height, this man slipped away unobserved, and I saw no more of him till he became my comrade on the sea. In a few minutes, however, he was missed by his shipmates, and being, it seems, for some reason a huge favourite with them, they raised a cry of "Bulkington! Bulkington! where's Bulkington?" and darted out of the house in pursuit of him.
It was now about nine o'clock, and the room seeming almost supernaturally quiet after these orgies, I began to congratulate myself upon a little plan that had occurred to me just previous to the entrance of the seamen.


Corporate Ipsum
Leverage agile frameworks to provide a robust synopsis for high level overviews. Iterative approaches to corporate strategy foster collaborative thinking to further the overall value proposition. Organically grow the holistic world view of disruptive innovation via workplace diversity and empowerment.
Bring to the table win-win survival strategies to ensure proactive domination. At the end of the day, going forward, a new normal that has evolved from generation X is on the runway heading towards a streamlined cloud solution. User generated content in real-time will have multiple touchpoints for offshoring.
Capitalise on low hanging fruit to identify a ballpark value added activity to beta test. Override the digital divide with additional clickthroughs from DevOps. Nanotechnology immersion along the information highway will close the loop on focusing solely on the bottom line.

                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ sudo apt install 7zip
[sudo] password for kali: 
7zip is already the newest version (26.03+dfsg-3).

┌──(kali㉿kali)-[~]
└─$ htop       
Command 'htop' not found, but can be installed with:
sudo apt install htop
Do you want to install it? (N/y)y
sudo apt install htop
Installing:
  htop
                                                                                                                                                                                                                                          
Suggested packages:
  strace

Summary:
  Upgrading: 0, Installing: 1, Removing: 0, Not Upgrading: 288
  Download size: 235 kB
  Space needed: 600 kB / 38.7 GB available

Get:1 http://kali.download/kali kali-rolling/main amd64 htop amd64 3.5.3-1 [235 kB]
Fetched 235 kB in 1s (371 kB/s)
Selecting previously unselected package htop.
(Reading database… 490858 files and directories currently installed.)
Preparing to unpack …/htop_3.5.3-1_amd64.deb…
Unpacking htop (3.5.3-1)…
Setting up htop (3.5.3-1)…
Processing triggers for mailcap (3.77)…
Processing triggers for kali-menu (2026.3.4)…
Processing triggers for desktop-file-utils (0.28-1)…
Processing triggers for hicolor-icon-theme (0.18-2)…
Processing triggers for man-db (2.12.0-3)…
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ htop
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ sudo apt install traceroute -y
traceroute is already the newest version (1:2.1.6-1).

Summary:
  Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: 288
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ traceroute google.com
traceroute to google.com (142.251.106.100), 30 hops max, 60 byte packets
 1  10.0.3.2 (10.0.3.2)  0.811 ms  0.772 ms  0.755 ms
 2  * * *
 3  * * *
 4  * * *
 5  * * *
 6  * * *
 7  * * *
 8  * * *
 9  * * *
10  * * *
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *

──(kali㉿kali)-[~]
└─$ sudo apt install nload -y
[sudo] password for kali:
Installing:
  nload
                                                                                                                                                                                                                                          
Summary:
  Upgrading: 0, Installing: 1, Removing: 0, Not Upgrading: 288
  Download size: 71.8 kB
  Space needed: 215 kB / 38.7 GB available

Get:1 http://http.kali.org/kali kali-rolling/main amd64 nload amd64 0.7.4+git20180309.8f92dc0-0.1 [71.8 kB]
Fetched 71.8 kB in 1s (72.0 kB/s)
Selecting previously unselected package nload.
(Reading database… 490869 files and directories currently installed.)
Preparing to unpack …/nload_0.7.4+git20180309.8f92dc0-0.1_amd64.deb…
Unpacking nload (0.7.4+git20180309.8f92dc0-0.1)…
Setting up nload (0.7.4+git20180309.8f92dc0-0.1)…
Processing triggers for kali-menu (2026.3.4)…
Processing triggers for man-db (2.12.0-3)…
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ nload
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ nload
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ strings /bin/ls | head

t/lib64/ld-linux-x86-64.so.2
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
fgetfilecon_raw
fgetfilecon
freecon
lgetfilecon
lgetfilecon_raw
optind
                                                                                                                                                                                                                                        
┌──(kali㉿kali)-[~]
└─$ speedtest-cli --secure
Retrieving speedtest.net configuration...
Testing from Pioneer Elabs (103.69.28.64)...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Hosted by Sat-Lines (Satpayev) [3595.84 km]: 250.819 ms
Testing download speed................................................................................
Download: 14.72 Mbit/s
Testing upload speed......................................................................................................
Upload: 13.15 Mbit/s

┌──(kali㉿kali)-[~]
└─$ sudo tcpdump -c 10
[sudo] password for kali: 
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
03:45:48.381369 IP 192.168.56.101.bootpc > 192.168.56.100.bootps: BOOTP/DHCP, Request from 08:00:27:a3:a0:09 (oui Unknown), length 282
03:45:48.392649 IP 192.168.56.100.bootps > 192.168.56.101.bootpc: BOOTP/DHCP, Reply, length 548
03:45:53.561802 ARP, Request who-has 192.168.56.100 tell 192.168.56.101, length 28
03:45:53.563000 ARP, Reply 192.168.56.100 is-at 08:00:27:5b:7e:1c (oui Unknown), length 46
03:47:15.978302 IP6 fe80::f938:74ef:df58:7f20 > ff02::1:ff00:1: ICMP6, neighbor solicitation, who has fe80::1, length 32
03:47:16.981492 IP6 fe80::f938:74ef:df58:7f20 > ff02::1:ff00:1: ICMP6, neighbor solicitation, who has fe80::1, length 32
03:47:17.977881 IP6 fe80::f938:74ef:df58:7f20 > ff02::1:ff00:1: ICMP6, neighbor solicitation, who has fe80::1, length 32
03:47:18.978628 IP6 fe80::f938:74ef:df58:7f20 > ff02::1:ff00:1: ICMP6, neighbor solicitation, who has fe80::1, length 32
03:49:25.978937 IP6 fe80::f938:74ef:df58:7f20 > ff02::1:ff00:1: ICMP6, neighbor solicitation, who has fe80::1, length 32
03:50:48.382200 IP 192.168.56.101.bootpc > 192.168.56.100.bootps: BOOTP/DHCP, Request from 08:00:27:a3:a0:09 (oui Unknown), length 282
10 packets captured
11 packets received by filter
0 packets dropped by kernel

                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ sudo nmap -O 192.168.56.101   # Kali ip
Starting Nmap 7.991 ( https://nmap.org ) at 2026-11-05 02:36 -0500
Stats: 0:00:35 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 25.37% done; ETC: 02:38 (0:01:43 remaining)
Nmap scan report for 192.168.56.101
Host is up (0.000047s latency).
All 1000 scanned ports on 192.168.56.101 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
Too many fingerprints match this host to give specific OS details
Network Distance: 0 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 204.60 seconds

┌──(kali㉿kali)-[~]
└─$ sudo nmap -O 192.168.56.102   # target metasploitable ip
[sudo] password for kali: 
Starting Nmap 7.991 ( https://nmap.org ) at 2026-11-05 03:26 -0500
Nmap scan report for 192.168.56.102
Host is up (0.00061s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 08:00:27:C7:FC:D6 (Oracle VirtualBox virtual NIC)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.991%E=4%D=11/5%OT=21%CT=1%CU=38745%PV=Y%DS=1%DC=D%G=Y%M=080027%
OS:TM=6AEC3DB5%P=x86_64-pc-linux-gnu)SEQ(SP=BC%GCD=1%ISR=B9%TI=Z%CI=Z%TS=7)
OS:SEQ(SP=BF%GCD=1%ISR=CC%TI=Z%CI=Z%TS=7)SEQ(SP=C4%GCD=1%ISR=C8%TI=Z%CI=Z%T
OS:S=7)SEQ(SP=C6%GCD=1%ISR=D2%TI=Z%CI=Z%TS=7)SEQ(SP=CE%GCD=1%ISR=D3%TI=Z%CI
OS:=Z%II=I%TS=7)OPS(O1=M5B4ST11NW7%O2=M5B4ST11NW7%O3=M5B4NNT11NW7%O4=M5B4ST
OS:11NW7%O5=M5B4ST11NW7%O6=M5B4ST11)WIN(W1=16A0%W2=16A0%W3=16A0%W4=16A0%W5=
OS:16A0%W6=16A0)ECN(R=Y%DF=Y%T=40%W=16D0%O=M5B4NNSNW7%CC=N%Q=)T1(R=Y%DF=Y%T
OS:=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=Y%DF=Y%T=40%W=16A0%S=O%A=S+%F=AS%O
OS:=M5B4ST11NW7%RD=0%Q=)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=B1C2A1A3%Q=)
OS:T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=B1C2A1A3%Q=)T6(R=Y%DF=Y%T=40%W=
OS:0%S=A%A=Z%F=R%O=%RD=B1C2A1A3%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD
OS:=B1C2A1A3%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%R
OS:UD=G)IE(R=N)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 1 hop

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.16 seconds

┌──(kali㉿kali)-[~]
└─$ nmap -p 1-65535 -T4 192.168.56.101   # Kali ip                             

Starting Nmap 7.991 ( https://nmap.org ) at 2026-11-05 03:53 -0500
Stats: 0:06:12 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 10.13% done; ETC: 04:55 (0:54:56 remaining)
Nmap scan report for 192.168.56.101
Host is up.
All 65535 scanned ports on 192.168.56.101 are in ignored states.
Not shown: 65535 filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 6583.75 seconds

┌──(kali㉿kali)-[~]
└─$ nmap -p 1-65535 -T4 192.168.56.102   # target metasploitable ip

Starting Nmap 7.991 ( https://nmap.org ) at 2026-11-07 02:09 -0500
Nmap scan report for 192.168.56.102
Host is up (0.00024s latency).
Not shown: 65505 closed tcp ports (reset)
PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
23/tcp    open  telnet
25/tcp    open  smtp
53/tcp    open  domain
80/tcp    open  http
111/tcp   open  rpcbind
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
512/tcp   open  exec
513/tcp   open  login
514/tcp   open  shell
1099/tcp  open  rmiregistry
1524/tcp  open  ingreslock
2049/tcp  open  nfs
2121/tcp  open  ccproxy-ftp
3306/tcp  open  mysql
3632/tcp  open  distccd
5432/tcp  open  postgresql
5900/tcp  open  vnc
6000/tcp  open  X11
6667/tcp  open  irc
6697/tcp  open  ircs-u
8009/tcp  open  ajp13
8180/tcp  open  unknown
8787/tcp  open  msgsrvr
42920/tcp open  unknown
48798/tcp open  unknown
53622/tcp open  unknown
58618/tcp open  unknown
MAC Address: 08:00:27:C7:FC:D6 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 2.65 seconds
                                                                

┌──(kali㉿kali)-[~]
└─$ nmap -sS -T4 192.168.56.101   # Kali ip
Starting Nmap 7.991 ( https://nmap.org ) at 2026-11-07 02:26 -0500
Nmap scan report for 192.168.56.101
Host is up.
All 1000 scanned ports on 192.168.56.101 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 102.35 seconds
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ nmap -sS -T4 192.168.56.102   # target metasploitable ip
Starting Nmap 7.991 ( https://nmap.org ) at 2026-11-07 02:29 -0500
Nmap scan report for 192.168.56.102
Host is up (0.00026s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 08:00:27:C7:FC:D6 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.70 seconds
                                                                  
┌──(kali㉿kali)-[~]
└─$ searchsploit wordpress ftp
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                                          |  Path
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
WordPress Plugin MiwoFTP 1.0.5 - Arbitrary File Download (1)                                                                                                                                            | php/webapps/36774.txt
WordPress Plugin MiwoFTP 1.0.5 - Arbitrary File Download (2)                                                                                                                                            | php/webapps/36801.txt
WordPress Plugin MiwoFTP 1.0.5 - Cross-Site Request Forgery / Arbitrary File Creation / Remote Code Execution                                                                                           | php/webapps/36763.txt
WordPress Plugin MiwoFTP 1.0.5 - Cross-Site Request Forgery / Arbitrary File Deletion                                                                                                                   | php/webapps/36761.txt
WordPress Plugin MiwoFTP 1.0.5 - Multiple Cross-Site Request Forgery / Cross-Site Scripting Vulnerabilities                                                                                             | php/webapps/36762.txt
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results


┌──(kali㉿kali)-[~]
└─$ dnsenum google.com
dnsenum VERSION:1.3.1

-----   google.com   -----


Host's addresses:
__________________

google.com.                              268      IN    A        142.250.206.174


Name Servers:
______________

ns3.google.com.                          21600    IN    A        216.239.36.10
ns1.google.com.                          21600    IN    A        216.239.32.10
ns2.google.com.                          21600    IN    A        216.239.34.10
ns4.google.com.                          21600    IN    A        216.239.38.10


Mail (MX) Servers:
___________________

smtp.google.com.                         300      IN    A        192.178.211.26
smtp.google.com.                         300      IN    A        192.178.211.27


Trying Zone Transfers and getting Bind Versions:
_________________________________________________


Trying Zone Transfer for google.com on ns3.google.com ... 
AXFR record query failed: corrupt packet

Trying Zone Transfer for google.com on ns1.google.com ... 
AXFR record query failed: corrupt packet

Trying Zone Transfer for google.com on ns2.google.com ... 
AXFR record query failed: corrupt packet

Trying Zone Transfer for google.com on ns4.google.com ... 
AXFR record query failed: corrupt packet


──(kali㉿kali)-[~]
└─$ lbd google.com        

lbd - load balancing detector 0.4 - Checks if a given domain uses load-balancing.
                                    Written by Stefan Behte (http://ge.mine.nu)
                                    Proof-of-concept! Might give false positives.

Checking for DNS-Loadbalancing: FOUND
google.com has address 142.250.134.113
google.com has address 142.250.134.102
google.com has address 142.250.134.139
google.com has address 142.250.134.138
google.com has address 142.250.134.100
google.com has address 142.250.134.101

Checking for HTTP-Loadbalancing [Server]: 
 gws
 NOT FOUND

Checking for HTTP-Loadbalancing [Date]: 08:27:44, 08:27:44, 08:27:44, 08:27:45, 08:27:45, 08:27:45, 08:27:46, 08:27:46, 08:27:46, 08:27:47, 08:27:47, 08:27:48, 08:27:48, 08:27:49, 08:27:49, 08:27:49, 08:27:50, 08:27:50, 08:27:51, 08:27:51, 08:27:51, 08:27:52, 08:27:52, 08:27:52, 08:27:53, 08:27:53, 08:27:54, 08:27:54, 08:27:55, 08:27:55, 08:27:55, 08:27:56, 08:27:56, 08:27:56, 08:27:57, 08:27:57, 08:27:57, 08:27:58, 08:27:58, 08:27:58, 08:27:59, 08:27:59, 08:27:59, 08:28:00, 08:28:00, 08:28:00, 08:28:01, 08:28:01, 08:28:01, 08:28:02, NOT FOUND

Checking for HTTP-Loadbalancing [Diff]: FOUND
< Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-szVFPGrWPeNeeoZNVljZ1g' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
> Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-C8pWVFFx3pYevjwfFxaNoA' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp

google.com does Load-balancing. Found via Methods: DNS HTTP[Diff]

┌──(kali㉿kali)-[~]
└─$ which nth          
/usr/bin/nth
                                                                                                                                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ nth -t ef487f75307f96954d3bb132e5f4b035

  _   _                           _____ _           _          _   _           _     
 | \ | |                         |_   _| |         | |        | | | |         | |    
 |  \| | __ _ _ __ ___   ___ ______| | | |__   __ _| |_ ______| |_| | __ _ ___| |__  
 | . ` |/ _` | '_ ` _ \ / _ \______| | | '_ \ / _` | __|______|  _  |/ _` / __| '_ \ 
 | |\  | (_| | | | | | |  __/      | | | | | | (_| | |_       | | | | (_| \__ \ | | |
 \_| \_/\__,_|_| |_| |_|\___|      \_/ |_| |_|\__,_|\__|      \_| |_/\__,_|___/_| |_|

https://twitter.com/bee_sec_san
https://github.com/HashPals/Name-That-Hash 
    

ef487f75307f96954d3bb132e5f4b035

Most Likely 
MD5, HC: 0 JtR: raw-md5 Summary: Used for Linux Shadow files.
MD4, HC: 900 JtR: raw-md4
NTLM, HC: 1000 JtR: nt Summary: Often used in Windows Active Directory.
Domain Cached Credentials, HC: 1100 JtR: mscach

Least Likely
Domain Cached Credentials 2, HC: 2100 JtR: mscach2 Double MD5, HC: 2600  Tiger-128,  Skein-256(128),  Skein-512(128),  Lotus Notes/Domino 5, HC: 8600 JtR: lotus5 md5(md5(md5($pass))), HC: 3500 Summary: Hashcat mode is only supported 
in hashcat-legacy. md5(uppercase(md5($pass))), HC: 4300  md5(sha1($pass)), HC: 4400  md5(utf16($pass)), JtR: dynamic_29 md4(utf16($pass)), JtR: dynamic_33 md5(md4($pass)), JtR: dynamic_34 Haval-128, JtR: haval-128-4 RIPEMD-128, JtR: 
ripemd-128 MD2, JtR: md2 Snefru-128, JtR: snefru-128 DNSSEC(NSEC3), HC: 8300  RAdmin v2.x, HC: 9900 JtR: radmin Cisco Type 7,  BigCrypt, JtR: bigcrypt
```

## 2. Reflection

### Why do we use Kali Linux? What is its advantage compared to other Linux distributions?

Kali Linux is a Linux distribution designed mainly for cybersecurity activities such as penetration testing, security research, digital forensics, and vulnerability assessment. Its main advantage over general-purpose distributions is that it provides a large collection of security tools and a security-testing-oriented environment. Tools can be used for network reconnaissance, traffic analysis, vulnerability research, and password auditing. Kali can also run in virtual machines, which makes it convenient for isolated and controlled labs.

### Which features and tools of Kali Linux attracted me the most?

The tools that attracted me most during this lab were:

- **Nmap:** identifies hosts, open ports, and services during network reconnaissance.
- **tcpdump:** captures packets and provides a command-line way to inspect network traffic.
- **htop and nload:** help monitor system processes/resources and network traffic in real time.
- **Searchsploit:** searches Exploit-DB for publicly documented vulnerabilities and exploits.
- **DNSenum:** enumerates DNS information and can discover subdomains.
- **LBD:** checks for indications of DNS or HTTP load balancing.
- **Name-That-Hash:** suggests possible hash algorithms from a hash value.

These tools helped me understand how different utilities support reconnaissance, network monitoring, and security assessment. The hands-on command-line work was particularly useful because it showed how security information can be collected and interpreted in Kali Linux.

## 3. Conclusion

This lab introduced me to Kali Linux, its command-line environment, system and network inspection commands, and several cybersecurity tools. I practiced collecting system information, downloading and inspecting a file, monitoring processes and traffic, scanning the lab target, searching vulnerability references, enumerating DNS information, detecting load-balancing indicators, and identifying possible hash types.
