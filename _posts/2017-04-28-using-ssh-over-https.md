---
layout: post
published: true
title: Using SSH over the HTTPS port
---


* Step 1: Edit your ssh local settings

```
vim ~/.ssh/config

```

with the following content

```
Host github.com
  Hostname ssh.github.com
  Port 443
```

* Step 2: Test it logging 

```
ssh -T -p 443 git@ssh.github.com
Hi username! You've successfully authenticated, but GitHub does not
provide shell access.
```

* Step 3: Test it clonning any repository

```
[root@pachacutec tmp]# git clone git@github.com:jenciso/jenciso.github.io.git    
Cloning into 'jenciso.github.io'...
The authenticity of host '[ssh.github.com]:443 ([192.30.253.122]:443)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[ssh.github.com]:443,[192.30.253.122]:443' (RSA) to the list of known hosts.
remote: Counting objects: 1957, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 1957 (delta 3), reused 0 (delta 0), pack-reused 1947
Receiving objects: 100% (1957/1957), 11.19 MiB | 2.47 MiB/s, done.
Resolving deltas: 100% (1133/1133), done.
[root@pachacutec tmp]# 
```

