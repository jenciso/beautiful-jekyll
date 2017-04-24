---
layout: post
published: true
title: Prepare windows machine to use ansible
bigimg: /img/ansible-windows-blog.png
---
## Prepare windows machine to use ansible

Open a window terminal in **powershell** as Administrator and run the following commands

```
PS C:\Windows\system32> cd C:\temp

PS C:\temp> Invoke-WebRequest -Uri https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1 -Method Get -OutFile ConfigureRemotingForAnsible.ps1

PS C:\temp> .\ConfigureRemotingForAnsible.ps1
```

If your server is behind of a proxy server, add to line 2:
```
-PassThru -Proxy http://ip_proxy_server:proxy_port
```

Example:
```
PS C:\temp> Invoke-WebRequest -Uri https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1 -Method Get -OutFile ConfigureRemotingForAnsible.ps1 -PassThru -Proxy http://192.168.0.20:8080
```
Result:

![powershell_ansible.png]({{site.baseurl}}/img/powershell_ansible.png)
