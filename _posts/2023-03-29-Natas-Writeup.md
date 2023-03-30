---
layout: default
title:  "Natas Writeup"
date:   2023-03-30 20:32:03 +0700
categories: ctf
---
# Natas Writeup

## Natas 0

Ctrl-U to see page source, we get the password for natas1: g9D9cREhslqBKtcA2uocGHPfMZVzeFK6

## Natas 1

Ctrl-U to see page source, we get the password for natas2: h4ubbcXrWqsTo7GGnnUMLppXbOogfBZ7

## Natas 2

Going to `website/files/`, we can see the users.txt file. Open this file, we can see password for natas3: `G6ctbMJ5Nb4cbFwhpMPSvxGHhQ7I6W8Q`

## Natas 3

Inspect index, we see the comment that say something about Google → search using google dork: `site:http://natas3.natas.labs.overthewire.org` → showing 1 result: [http://natas3.natas.labs.overthewire.org/s3cr3t](http://natas3.natas.labs.overthewire.org/s3cr3t) → open users.txt, we get the password for natas4: `tKOcJIbzM4lTs8hbCmzn5Zr4434fGZQm`

## Natas 4

Using Burp to catch request, change the Referer header of GET request to natas5… → we get the password of natas5: Z0NsrtIkJoKALBCLi5eqFfcRN82Au2oD

## Natas 5

Using Burp to catch request,  we found 2 responses. The 1st response return “401 Unauthorized”, and the 2nd response has a SetCookie with loggedin=0 → add the Cookie header of GET request with “loggedin=1” → we get the password of natas6: `fOIvE0MDtPTgRhqmmvvAOt2EfXR6uQgR`

## Natas 6

Checking source code of the website, we see a line that include a file called `secret.inc`. Going to this file: [`http://natas6.natas.labs.overthewire.org/includes/secret.inc`](http://natas6.natas.labs.overthewire.org/includes/secret.inc), we found the secret: `FOEIUWGHFEEUHOFUOIU`. Input the secret, we get the password of natas7: `jmxSiH3SP6Sonf8dv66ng8v1cIEdjXWr`

## Natas 7

Checking the source code of the website, we see a hint that the pass will be on the directory `/etc/natas_webpass/natas8`. Back to the home page, when I go to the links , the URL for this is [`http://natas7.natas.labs.overthewire.org/index.php?page=home`](http://natas7.natas.labs.overthewire.org/index.php?page=home). Change the URL to [http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8](http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8), we get the password of natas8: `a6bZCNYwdKqN5cGP11ZdtPg0iImQQhAB`

## Natas 8

Checking the source code of the website, we see a function that encode the secret with the secret encoded:

```php
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}
```

→ `hex2bin(strrev(base64_decode($secret))` to get the decoded secret: `oubWYf2kBq` . Enter the secret, we get the password for natas9: `Sda6t0vkOPkM8YeOZkAGVhFoaplvlJFd`  

## Natas9

- Checking the input box by typing random command, we can see that this website is vulnerable by directory traversal, example `a;ls ../../../../home` will list all the file on `/home` on this server.
- Deep digging inside this server, we can see a folder named `natas_webpass` in `/etc`. Checking this folder, we see that this has all password for all natas level. So, we use command to get the password of natas10: `a;cat ../../../../etc/natas_webpass/natas10` → password: `D44EcsFkLxPIkAAKLosx8z3hxX1Z4MCE`

## Natas10

-