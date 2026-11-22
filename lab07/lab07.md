# Lab 07: Verifying Software Integrity (SHA256 & GPG)

## Objectives

-   Verify file integrity using SHA256 checksums.
-   Understand why checksums alone are not enough.
-   Use GPG to sign and verify files.
-   Detect tampered software before execution.
-   Apply secure practices when downloading scripts.

## Background

When downloading scripts or software, the file may have been modified,
replaced by a malicious version, or obtained from an untrusted source.

This lab uses:

-   **SHA256 checksums** to detect changes to file contents.
-   **GPG digital signatures** to verify that signed content matches the
    signing key.

## Lab Environment

  Item                Details
  ------------------- ----------------------------
  Operating system    Kali Linux
  Working directory   `/home/kali/CS-Vaje/lab07`
  GPG version         2.4.9
  GNU coreutils       9.10
  Provided file       `install.sh`

All terminal sessions below show each command (after the `└─$` prompt)
followed directly by its output, copied from the terminal.

------------------------------------------------------------------------

## Task 1: Inspect the Script

The repository was updated and the lab directory opened. The script was
inspected before anything was executed.

``` text
┌──(kali㉿kali)-[~]
└─$ cd CS-Vaje

┌──(kali㉿kali)-[~/CS-Vaje]
└─$ git pull origin main
From https://github.com/mohammedmoiz951-maker/CS-Vaje
 * branch            main       -> FETCH_HEAD
Already up to date.

┌──(kali㉿kali)-[~/CS-Vaje]
└─$ cd lab07

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ cat install.sh
echo "Installing demo software ..."
mkdir src
touch run.sh
echo "echo Hello" > run.sh
mv run.sh src
sh src/run.sh

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ pwd
/home/kali/CS-Vaje/lab07

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ ls -la
total 16
drwxrwxr-x  2 kali kali 4096 Nov  1 08:40 .
drwxrwxr-x 12 kali kali 4096 Nov  1 08:40 ..
-rw-rw-r--  1 kali kali  113 Nov  1 08:40 install.sh
-rw-rw-r--  1 kali kali 3248 Nov  1 08:40 README.md
```

### What does this script do?

1.  Displays the message `Installing demo software ...`.
2.  Creates a directory named `src`.
3.  Creates an empty file named `run.sh`.
4.  Writes the command `echo Hello` into `run.sh`.
5.  Moves `run.sh` into the `src` directory.
6.  Executes `src/run.sh`, which displays `Hello`.

The script does not use sudo or make network connections. It performs basic file and directory operations in the current working directory and executes a secondary shell script. Although this script is benign in the lab environment, inspecting commands before execution is an important security practice because scripts can perform unexpected or harmful actions.

### Required packages

The package installation command from the lab was run:

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ sudo apt install gnupg coreutils -y
[sudo] password for kali:
coreutils is already the newest version (9.10-1).
[... apt "no longer required" package list omitted ...]
```

`gnupg` and `coreutils` were already installed on the Kali system, so
nothing new was installed. The version checks in Task 2 confirm that both
tools are available.

**Screenshot:**
`screenshots/screenshot01-setup-and-script-inspection.png`

------------------------------------------------------------------------

## Task 2: Generate a SHA256 Checksum

The installed versions of GPG and SHA256 were checked, then the checksum
was generated and saved.

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ gpg --version

gpg (GnuPG) 2.4.9
libgcrypt 1.12.4
Copyright (C) 2025 g10 Code GmbH
License GNU GPL-3.0-or-later <https://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Home: /home/kali/.gnupg
Supported algorithms:
Pubkey: RSA, ELG, DSA, ECDH, ECDSA, EDDSA
Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
        CAMELLIA128, CAMELLIA192, CAMELLIA256
Hash: SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
Compression: Uncompressed, ZIP, ZLIB, BZIP2

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ sha256sum --version
sha256sum (GNU coreutils) 9.10
Packaged by Debian (9.10-1)
Copyright (C) 2026 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Written by Ulrich Drepper, Scott Miller, and David Madore.

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ sha256sum install.sh > install.sh.sha256

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ cat install.sh.sha256
e277935b53a8b2bec27536e89fdfd5e72e67b6b5034ce3d985fef89c70d438e3  install.sh

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ ls -lh
total 12K
-rw-rw-r-- 1 kali kali  113 Nov  1 08:40 install.sh
-rw-rw-r-- 1 kali kali   77 Nov 18 16:58 install.sh.sha256
-rw-rw-r-- 1 kali kali 3.2K Nov  1 08:40 README.md
```

The checksum represents the contents of `install.sh` at the time it was
generated.

**Screenshot:**
`screenshots/screenshot02-sha256-generation-and-check.png`

------------------------------------------------------------------------

## Task 3: Verify File Integrity

The generated checksum was checked against the current script.

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ sha256sum -c install.sh.sha256
install.sh: OK
```

The calculated hash matched the saved hash, so the script had not
changed since the checksum was generated.

**Screenshot:**
`screenshots/screenshot02-sha256-generation-and-check.png`

------------------------------------------------------------------------

## Task 4: Generate a GPG Key Pair

A GPG key pair was generated with the following choices: RSA and RSA,
4096 bits, a validity of 1 year (my own choice; the lab does not specify
an expiry), name `moizuddin` and email `moizuddin@example.com`.

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ gpg --full-generate-key
gpg (GnuPG) 2.4.9; Copyright (C) 2025 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (9) ECC (sign and encrypt) *default*
  (10) ECC (sign only)
  (14) Existing key from card
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 1y
Key expires at Thu 18 Nov 2027 05:02:44 PM EST
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: moizuddin
Email address: moizuddin@example.com
Comment: 
You selected this USER-ID:
    "moizuddin <moizuddin@example.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: WARNING: server 'gpg-agent' is older than us (2.2.40 < 2.4.9)
gpg: Note: Outdated servers may lack important security fixes.
gpg: Note: Use the command "gpgconf --kill all" to restart them.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: revocation certificate stored as '/home/kali/.gnupg/openpgp-revocs.d/2B71299463C3624C78E7CC6C4E276ABAE29BB95E.rev'
public and secret key created and signed.

pub   rsa4096 2026-11-18 [SC] [expires: 2027-11-18]
      2B71299463C3624C78E7CC6C4E276ABAE29BB95E
uid                      moizuddin <moizuddin@example.com>
sub   rsa4096 2026-11-18 [E] [expires: 2027-11-18]
```

GnuPG also created a revocation certificate (the `.rev` file). It can be
used to invalidate the key if the private key is ever lost or leaked.

**Screenshot:** `screenshots/screenshot03-gpg-key-generation.png`

The public and secret keys were then listed (a personal email address in
the keyring is redacted below).

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ gpg --list-keys
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   3  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 3u
gpg: next trustdb check due at 2027-11-11
/home/kali/.gnupg/pubring.kbx
-----------------------------
pub   rsa4096 2026-11-11 [SC] [expires: 2027-11-11]
      93133F9D903B3783E5AFE71C7A543728FC6CE7ED
uid           [ultimate] Mohammed Moiz Uddin <[personal email redacted]>
sub   rsa4096 2026-11-11 [E] [expires: 2027-11-11]

pub   rsa4096 2026-11-12 [SC] [expires: 2027-11-12]
      0E8979ECC0E9193FA8E4F6773F2DCC9C67AE1094
uid           [ultimate] Peer User <peer@example.com>
sub   rsa4096 2026-11-12 [E] [expires: 2027-11-12]

pub   rsa4096 2026-11-18 [SC] [expires: 2027-11-18]
      2B71299463C3624C78E7CC6C4E276ABAE29BB95E
uid           [ultimate] moizuddin <moizuddin@example.com>
sub   rsa4096 2026-11-18 [E] [expires: 2027-11-18]

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ gpg --list-secret-keys --keyid-format LONG
gpg: WARNING: server 'gpg-agent' is older than us (2.2.40 < 2.4.9)
gpg: Note: Outdated servers may lack important security fixes.
gpg: Note: Use the command "gpgconf --kill all" to restart them.
gpg: problem with fast path key listing: IPC parameter error - ignored
/home/kali/.gnupg/pubring.kbx
-----------------------------
sec   rsa4096/7A543728FC6CE7ED 2026-11-11 [SC] [expires: 2027-11-11]
      93133F9D903B3783E5AFE71C7A543728FC6CE7ED
uid                 [ultimate] Mohammed Moiz Uddin <[personal email redacted]>
ssb   rsa4096/640A8AF2C9A6E78C 2026-11-11 [E] [expires: 2027-11-11]

sec   rsa4096/3F2DCC9C67AE1094 2026-11-12 [SC] [expires: 2027-11-12]
      0E8979ECC0E9193FA8E4F6773F2DCC9C67AE1094
uid                 [ultimate] Peer User <peer@example.com>
ssb   rsa4096/99571D50F31F6138 2026-11-12 [E] [expires: 2027-11-12]

sec   rsa4096/4E276ABAE29BB95E 2026-11-18 [SC] [expires: 2027-11-18]
      2B71299463C3624C78E7CC6C4E276ABAE29BB95E
uid                 [ultimate] moizuddin <moizuddin@example.com>
ssb   rsa4096/095314C43F365287 2026-11-18 [E] [expires: 2027-11-18]
```

The keyring contains three secret keys: two from earlier work and the new
key for this lab. Because several secret keys exist, `--local-user` is
used in Task 5 so that the correct key signs the file. The key used for
this lab is:

  Field         Value
  ------------- --------------------------------------------
  User ID       `moizuddin <moizuddin@example.com>`
  Algorithm     RSA 4096
  Long key ID   `4E276ABAE29BB95E`
  Fingerprint   `2B71299463C3624C78E7CC6C4E276ABAE29BB95E`
  Expiration    18 November 2027

An outdated `gpg-agent` warning appeared during key generation and key
listing. The agent was restarted before signing:

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ gpgconf --kill all
```

**Screenshot:** `screenshots/screenshot04-gpg-key-listing.png`

------------------------------------------------------------------------

## Task 5: Sign the Checksum File

The checksum file was signed using the generated GPG secret key, and the
resulting files were listed.

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ gpg --local-user 4E276ABAE29BB95E --detach-sign install.sh.sha256

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ ls -lh install.sh.sha256*
-rw-rw-r-- 1 kali kali  77 Nov 18 16:58 install.sh.sha256
-rw-rw-r-- 1 kali kali 566 Nov 18 17:08 install.sh.sha256.sig
```

The detached signature `install.sh.sha256.sig` was created successfully.

**Screenshot:**
`screenshots/screenshot05-signature-tampering-and-safe-execution.png`

------------------------------------------------------------------------

## Task 6: Verify the GPG Signature

The signature was verified against the checksum file.

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ gpg --verify install.sh.sha256.sig install.sh.sha256
gpg: Signature made Wed 18 Nov 2026 05:08:39 PM EST
gpg:                using RSA key 2B71299463C3624C78E7CC6C4E276ABAE29BB95E
gpg: Good signature from "moizuddin <moizuddin@example.com>" [ultimate]
```

GPG reported a good signature. This means the checksum file matched the
content covered by the signature, and the signature corresponded to the
public key in the local keyring. The key shows `[ultimate]` trust because
it was generated on this machine, so no "not certified" warning appeared.

For real software downloads, the publisher's public key must be obtained
and authenticated independently. A good signature from a locally
generated key alone does not prove that an external publisher is
trustworthy.

**Screenshot:**
`screenshots/screenshot05-signature-tampering-and-safe-execution.png`

------------------------------------------------------------------------

## Task 7: Simulate a Tampering Attack

An additional command was appended to the installation script to
simulate tampering, the modified script was inspected, and the checksum
was checked again.

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ echo 'echo MALICIOUS CODE EXECUTED' >> install.sh

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ cat install.sh
echo "Installing demo software ..."
mkdir src
touch run.sh
echo "echo Hello" > run.sh
mv run.sh src
sh src/run.shecho MALICIOUS CODE EXECUTED

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ sha256sum -c install.sh.sha256
install.sh: FAILED
sha256sum: WARNING: 1 computed checksum did NOT match
```

The checksum verification failed because the modified file no longer
matched the original saved checksum. The modified script was not
executed.

The original script did not end with a newline, so the appended text was
joined to the last line (`sh src/run.shecho MALICIOUS CODE EXECUTED`).
The file contents still changed, which is all the checksum needs to
detect. However, the appended text did not become a separate command, so
it would not have run as intended. A real attacker would add a newline
first (for example with
`printf '\necho MALICIOUS CODE EXECUTED\n' >> install.sh`).

The original script was then restored from Git:

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ git restore install.sh
```

**Screenshot:**
`screenshots/screenshot05-signature-tampering-and-safe-execution.png`

------------------------------------------------------------------------

## Task 8: Safe Execution Workflow

After restoring the original script, the checksum and signature were
verified again. The script was executed only after both checks
succeeded.

``` text
┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ sha256sum -c install.sh.sha256
install.sh: OK

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ gpg --verify install.sh.sha256.sig install.sh.sha256
gpg: Signature made Wed 18 Nov 2026 05:08:39 PM EST
gpg:                using RSA key 2B71299463C3624C78E7CC6C4E276ABAE29BB95E
gpg: Good signature from "moizuddin <moizuddin@example.com>" [ultimate]

┌──(kali㉿kali)-[~/CS-Vaje/lab07]
└─$ bash install.sh
Installing demo software ...
Hello
```

Both verification checks succeeded, and the original installation script
executed successfully.

**Screenshot:**
`screenshots/screenshot05-signature-tampering-and-safe-execution.png`

------------------------------------------------------------------------

## Questions and Answers

### 1. Why should you never execute scripts without inspection?

A script runs with the privileges of the user who starts it, possibly
root if it is used with `sudo`. It can modify or delete files, change
system settings, download and execute other programs, or expose
sensitive information, and nothing stops it once it has started.
Inspecting it first (here with `cat install.sh`) shows what it will do
and whether it contains suspicious operations such as downloads, `sudo`,
`rm`, or obfuscated code.

### 2. What does SHA256 guarantee?

SHA256 produces a cryptographic hash of the file's contents. Comparing
the calculated hash with a trusted reference hash shows whether the file
has changed: any modification, even a single bit, produces a different
hash. It guarantees integrity only. By itself it does not identify the
author or prove where the file came from.

### 3. What does GPG guarantee?

When a signature verifies correctly, GPG confirms that the signed
content has not changed since it was signed and that the signature was
made with the private key corresponding to the verifying public key.
The publisher's identity is trustworthy only if the public key itself
has been authenticated (for example by checking its fingerprint through
an independent channel, or through the Web of Trust).

### 4. Can SHA256 prove the author of a file?

No. SHA256 is a hash function, not a digital signature. Anyone can
calculate a SHA256 hash for any file. There is no secret key or identity
involved, so a hash says nothing about who created or published the
file.

### 5. Why is signing the checksum important?

A checksum file stored next to a download can be replaced by the same
attacker who replaced the file. The attacker modifies the script, runs
`sha256sum` on the modified version, and publishes the new checksum, and
`sha256sum -c` then reports `OK` for the malicious file. Signing the
checksum with GPG links it to the author's private key, which the
attacker does not have, so a forged checksum fails signature
verification. Signing the small checksum file rather than the whole
download is also more practical. As noted in Task 6, this only works if
the public key used for verification has been obtained and authenticated
independently.

### 6. What happened after the script was modified?

After an extra command was appended to `install.sh`, its calculated
SHA256 hash no longer matched the saved checksum, and
`sha256sum -c install.sh.sha256` reported `install.sh: FAILED` with a
warning that 1 computed checksum did not match. The tampering was
therefore detected before the script was executed. SHA256 only shows
that the file changed; it cannot say who changed it or why. The original
script was then restored from Git, its checksum and signature were
verified successfully, and the restored script was executed.

------------------------------------------------------------------------

## Conclusion

In this lab, SHA256 was used to generate and verify a checksum for the
provided installation script. A 4096-bit RSA GPG key pair was generated,
and the checksum file was digitally signed and successfully verified. A
tampering attempt caused checksum verification to fail. After restoring
the original script, both the checksum and GPG signature checks
succeeded, and the script executed successfully.

The lab demonstrated how checksums help detect changes and how digital
signatures allow signed data to be verified against a particular signing
key, and why the checksum itself must be signed so that an attacker
cannot replace both the file and its checksum.
