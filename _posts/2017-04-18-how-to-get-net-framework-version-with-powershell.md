---
layout: post
published: true
title: How to get .Net Framework version with PowerShell
bigim: /img/dotnet.jpg
---
Open one powershell window and execute this command:

```
Get-ChildItem 'HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP' -recurse |
Get-ItemProperty -name Version,Release -EA 0 |
Where { $_.PSChildName -match '^(?!S)\p{L}'} |
Select PSChildName, Version, Release
```

Based on the MSDN article, you could add a switch to return the marketing product version number for releases after 4.5:

```
Get-ChildItem 'HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP' -recurse |
Get-ItemProperty -name Version,Release -EA 0 |
Where { $_.PSChildName -match '^(?!S)\p{L}'} |
Select PSChildName, Version, Release, @{
  name="Product"
  expression={
      switch($_.Release) {
        378389 { [Version]"4.5" }
        378675 { [Version]"4.5.1" }
        378758 { [Version]"4.5.1" }
        379893 { [Version]"4.5.2" }
        393295 { [Version]"4.6" }
        393297 { [Version]"4.6" }
        394254 { [Version]"4.6.1" }
        394271 { [Version]"4.6.1" }
      }
    }
}

```

