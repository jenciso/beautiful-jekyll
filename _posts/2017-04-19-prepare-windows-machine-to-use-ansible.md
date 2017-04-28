---
layout: post
published: true
title: Prepare windows machine to use ansible
bigimg: /img/ansible-windows-blog.png
---
## Prepare windows machine to use ansible

* Step 1: Open a window terminal in **powershell** as Administrator and run the following commands

```
PS C:\Windows\system32> cd C:\temp

PS C:\temp> Invoke-WebRequest -Uri https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1 -Method Get -OutFile ConfigureRemotingForAnsible.ps1
```

* Step 2: Execute the script file

PS C:\temp> .\ConfigureRemotingForAnsible.ps1
```

If your server is behind of a proxy server, add the following parameter to line 2:

```
-PassThru -Proxy http://ip_proxy_server:proxy_port
```

Example:
```
PS C:\temp> Invoke-WebRequest -Uri https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1 -Method Get -OutFile ConfigureRemotingForAnsible.ps1 -PassThru -Proxy http://192.168.0.20:8080
```
Result:

![powershell_ansible.png]({{site.baseurl}}/img/powershell_ansible.png)


* Step 3: If the script show a error message like this:

```
.\ConfigureRemotingForAnsible.ps1
		
# .\ConfigureRemotingForAnsible.ps1 : File 
# .\ConfigureRemotingForAnsible.ps1 cannot be loaded
# because running scripts is disabled on this system. For 
# more information, see about_Execution_Policies at
# http://go.microsoft.com/fwlink/?LinkID=135170.
# At line:1 char:1
# + .\ConfigureRemotingForAnsible.ps1
# + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#	+ CategoryInfo : SecurityError: (:) [], PSSecurityException
#		+ FullyQualifiedErrorId : UnauthorizedAccess
```

then, check your user scope is by running this:

```
Get-ExecutionPolicy -Scope CurrentUser
	
# Undefined
```

To fix the problem, run this:

```
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned

# Execution Policy Change
# The execution policy helps protect you from scripts that 
# you do not trust. Changing the execution policy might expose
# you to the security risks described in the 
# about_Execution_Policies help topic at
# http://go.microsoft.com/fwlink/?LinkID=135170. Do you want 
# to change the execution policy?
# [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
```
and response the Answer to Y 


Here you have more tips:

http://damonoverboe.org/devops/ci/continuous-delivery/ansible/windows/2014/08/25/ansibleWindows.html

