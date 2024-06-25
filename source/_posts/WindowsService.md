---
title: WindowsService
date: 2023-02-17 15:26:13
tags: 学无止境
---

# Windows Service程序

## 安装、拆卸、调试Windows服务

### 1、安装

```c
New-Service -Name "WorkingHoursDataSyncer" -BinaryPathName "C:\Working Hour Data Syncer\WorkingHoursDataSyncer.exe"

或者：
sc.exe create DowntimeMonitor binPath= "C:\Caroline File\DowntimeMonitorService\NewDowntimeIncidentMonitorService.exe" DisplayName= "Downtime Monitor Service" start= auto 

sc.exe start DowntimeMonitor

```

### 2、拆卸

- 查看PowerShell版本 ```$PSVersionTable```
- PowerShell V6.0及以上 ```Remove-Service 服务名 -Confirm:$false -Verbose```
-  PowerShell V5.1或更低版本 ```Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\服务名 | Remove-Item -Force -Verbose``` -> ```sc.exe delete "服务名"```

### 3、调试

- 将 Windows服务，改成 Console 程序调试。具体步骤参考[如何：调试 Windows 服务应用程序](https://learn.microsoft.com/zh-cn/dotnet/framework/windows-services/how-to-debug-windows-service-applications)


## Q&A

**1、 windows服务启动时：The system cannot find the file specified.**

在 properties 查看该服务的运行路径是否是完整路径，如果不是，拆卸当前服务，重新安装

```c
New-Service -Name "WorkingHoursDataSyncer" -BinaryPathName "C:\Working Hour Data Syncer\WorkingHoursDataSyncer.exe"
```

在 ```BinaryPathName``` 中使用完整路径。

## 参考文档

[1、如何：安装和卸载 Windows 服务](https://learn.microsoft.com/zh-cn/dotnet/framework/windows-services/how-to-install-and-uninstall-services)
[2、如何使用PowerShell删除Windows服务](https://www.mianshigee.com/note/detail/116499afo/)
[3、查看PowerShell版本](https://jingyan.baidu.com/article/6c67b1d68c70be6687bb1ee8.html)
[4、如何：调试 Windows 服务应用程序](https://learn.microsoft.com/zh-cn/dotnet/framework/windows-services/how-to-debug-windows-service-applications)