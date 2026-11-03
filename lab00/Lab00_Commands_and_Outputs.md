# Lab 00 — Introduction to Linux: Basics of Working in the Command Line

## Environment
- OS: Kali GNU/Linux (VirtualBox)
- User: `kali`
- Working directory: `/home/kali/linux-exercise`

This document records the commands and terminal outputs provided from the lab. Outputs are transcribed from the user's terminal; no output has been invented.

## 1. Navigation

```console
┌──(kali㉿kali)-[~]
└─$ pwd
/home/kali

┌──(kali㉿kali)-[~]
└─$ mkdir linux-exercise

┌──(kali㉿kali)-[~]
└─$ cd linux-exercise

┌──(kali㉿kali)-[~/linux-exercise]
└─$ ls -l
total 0

┌──(kali㉿kali)-[~/linux-exercise]
└─$ ls -la
total 8
drwxrwxr-x  2 kali kali 4096 Nov  3 01:57 .
drwx------ 47 kali kali 4096 Nov  3 01:57 ..

┌──(kali㉿kali)-[~/linux-exercise]
└─$ pwd
/home/kali/linux-exercise
```

**Explanation:** `pwd` prints the current directory; `mkdir` creates a directory; `cd` changes directory; `ls -l` displays a detailed listing; `ls -la` also shows hidden entries (`.` and `..`).

## 2. Create, inspect, and organize files

```console
┌──(kali㉿kali)-[~/linux-exercise]
└─$ echo "Mohammed Moiz Uddin" > description.txt

┌──(kali㉿kali)-[~/linux-exercise]
└─$ cat description.txt
Mohammed Moiz Uddin

┌──(kali㉿kali)-[~/linux-exercise]
└─$ mkdir test

┌──(kali㉿kali)-[~/linux-exercise]
└─$ mv description.txt test/

┌──(kali㉿kali)-[~/linux-exercise]
└─$ ls -l test
total 4
-rw-rw-r-- 1 kali kali 20 Nov  3 01:58 description.txt

┌──(kali㉿kali)-[~/linux-exercise]
└─$ mv test/description.txt test/my_profile.txt

┌──(kali㉿kali)-[~/linux-exercise]
└─$ ls -l test
total 4
-rw-rw-r-- 1 kali kali 20 Nov  3 01:58 my_profile.txt
```

**Explanation:** `echo ... > file` writes text into a file; `cat` displays its contents; `mkdir` creates `test`; `mv` moves or renames a file; `ls -l` verifies the result.

## 3. Copy the profile file to the home directory

```console
┌──(kali㉿kali)-[~/linux-exercise]
└─$ cp test/my_profile.txt ~/

┌──(kali㉿kali)-[~/linux-exercise]
└─$ ls -l ~/my_profile.txt
-rw-rw-r-- 1 kali kali 20 Nov  3 02:01 /home/kali/my_profile.txt
```

**Explanation:** `cp` copies the profile file into the home directory (`~/`). `ls -l ~/my_profile.txt` verifies the copied file.

## 4. Check sizes and change permissions

```console
┌──(kali㉿kali)-[~/linux-exercise]
└─$ ls -lh
total 4.0K
drwxrwxr-x 2 kali kali 4.0K Nov  3 02:00 test

┌──(kali㉿kali)-[~/linux-exercise]
└─$ du -sh ./*
8.0K    ./test

┌──(kali㉿kali)-[~/linux-exercise]
└─$ chmod 444 test/my_profile.txt

┌──(kali㉿kali)-[~/linux-exercise]
└─$ ls -l test/my_profile.txt
-r--r--r-- 1 kali kali 20 Nov  3 01:58 test/my_profile.txt
```

**Explanation:** `ls -lh` gives a human-readable listing; `du -sh ./*` reports the size of each item in the current directory; `chmod 444` makes the file readable by owner, group, and others, without write or execute permission. The final listing confirms the permissions.

## 5. System information and disk usage

```console
┌──(kali㉿kali)-[~/linux-exercise]
└─$ cd

┌──(kali㉿kali)-[~]
└─$ whoami
kali

┌──(kali㉿kali)-[~]
└─$ uname -a
Linux kali 7.1.5+kali-amd64 #1 SMP PREEMPT_DYNAMIC Kali 7.1.5-1kali1 (2026-07-29) x86_64 GNU/Linux

┌──(kali㉿kali)-[~]
└─$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            934M     0  934M   0% /dev
tmpfs           197M  980K  196M   1% /run
/dev/sda1        79G   39G   37G  52% /
tmpfs           985M  4.0K  985M   1% /dev/shm
tmpfs           985M  208K  985M   1% /tmp
none            1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
tmpfs           197M  100K  197M   1% /run/user/1000
none            1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
```

**Explanation:** `cd` without an argument returns to the home directory; `whoami` prints the current username; `uname -a` shows system/kernel details; `df -h` displays filesystem capacity and free space in human-readable units.

## 6. Extra task — largest entries in the home directory

```console
┌──(kali㉿kali)-[~]
└─$ du -ah ~ | sort -rh | head -n 5
9.2G    /home/kali
4.1G    /home/kali/Desktop/liveips.txt
4.1G    /home/kali/Desktop
1.9G    /home/kali/test1.txt
1.1G    /home/kali/.cache/mozilla/firefox/pozemcn3.default-esr
```

**Explanation:** `du -ah ~` lists file and directory sizes under the home directory; `sort -rh` sorts by size in reverse human-readable order; `head -n 5` prints the first five entries. The output contains both files and directories.

## Conclusion
The lab covered directory navigation, creating and inspecting files, moving and copying files, changing permissions, checking system information and disk usage, and finding large files/directories. The command/output transcript above documents the results provided.
