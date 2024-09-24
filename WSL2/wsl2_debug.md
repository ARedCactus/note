# 2021 WSL2 安装/修复

打开Windows PoweShell(管理员)依次执行，完成后==重启计算机==：
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

打开Windows PoweShell(管理员)执行以下命令，设置wsl新版：
```
wsl --set-default-version 2
```

下载[适用于 x64 计算机的 WSL2 Linux 内核更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)并且安装，然后再启动你在win应用商店下载的子系统发行版就okk



