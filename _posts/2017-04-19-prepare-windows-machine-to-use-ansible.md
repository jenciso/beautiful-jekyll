---
layout: post
published: true
title: Prepare windows machine to use ansible
bigimg: /img/ansible-windows-blog.png
---
## Prepare windows machine to use ansible

Step 1: Open a window powershell as Administrator and execute the following commands

```
PS C:\Windows\system32> cd C:\temp

PS C:\temp> Invoke-WebRequest -Uri https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1 -Method Get -OutFile ConfigureRemotingForAnsible.ps1 -PassThru -Proxy http://192.168.0.20:8080

PS C:\temp> .\ConfigureRemotingForAnsible.ps1
```
