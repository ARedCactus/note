## *列出所有虚拟交换机*
Windows 管理员方式运行PowerShell
```
Get-VMSwitch
```

如果仅需要列出使用了 `外部网络` 的虚拟交换机，可以增加命令参数：`-SwitchType External`
```
Get-VMSwitch -SwitchType External
```

## *列出所有网络适配器*
```
Get-NetAdapter
```


### 显示隐藏netadapter
- vEthernet (WSL (Hyper-V firewall))
```
ipconfig /all
```

### 添加入站规则 (vEthernet(WSL))
```
New-NetFirewallRule -DisplayName "WSL" -Direction Inbound  -InterfaceAlias "vEthernet (WSL (Hyper-V firewall))"  -Action Allow
```

## *Nat模式*
确定 IP 地址（用于通过 WSL 运行的 Linux 分发）时，需要考虑两种场景：

场景一：从 Windows 主机的角度来看，你想要查询通过 WSL2 运行的 Linux 分发的 IP 地址，使 Windows 主机上的程序可连接到分发（实例）中运行的服务器程序。

Windows 主机可使用命令：

复制

```
wsl -d <DistributionName> hostname -I
```

如果查询默认分发，则可省略指定该分发的此部分命令：`-d <DistributionName>`。 请务必使用大写 `-I` 标志，而不是小写 `-i`。

在后台，主机命令 `wsl.exe` 启动目标实例并执行 Linux 命令 `hostname -I`。 然后，此命令将 WSL 实例的 IP 地址打印到 `STDOUT`。 `STDOUT` 文本内容随后被中继回 wsl.exe。 最后，wsl.exe 显示该命令行的输出。

典型的输出可能为：

PowerShell复制

```
172.30.98.229
```

场景二：通过 WSL2（实例）在 Linux 分发中运行的程序想知道 Windows 主机的 IP 地址，使 Linux 程序可连接到 Windows 主机服务器程序。

WSL2 Linux 用户可使用命令：

Bash复制

```
ip route show | grep -i default | awk '{ print $3}'
```

典型的输出可能为：

复制

```
172.30.96.1
```

因此，在本示例中，`172.30.96.1` 是 Windows 的主机 IP 地址。

 备注

当 WSL2 以默认 [NAT 网络模式](https://learn.microsoft.com/zh-cn/windows/wsl/networking#default-networking-mode-nat)运行时，通常需要上述 IP 地址查询操作。 当 WSL2 以新的[镜像模式](https://learn.microsoft.com/zh-cn/windows/wsl/networking#mirrored-mode-networking)运行时，Windows 主机和 WSL2 VM 可使用 `localhost` (127.0.0.1) 作为目标地址相互连接，因此不需要使用查询对等机的 IP 地址。

## *桥接模式网络*
- ~/.wslconfig
```
networkingMode=bridged
vmSwitch=WSLBridge
ipv6=true
dnsTunneling=true
firewall=true
autoProxy=true
```

## *镜像模式网络*
在运行 Windows 11 22H2 及更高版本的计算机上，可以[在 `.wslconfig` 文件中的 `[wsl2]` 下设置 `networkingMode=mirrored`](https://learn.microsoft.com/zh-cn/windows/wsl/wsl-config#configuration-settings-for-wslconfig)，以启用镜像模式网络。 启用此功能会将 WSL 更改为全新的网络体系结构，其目标是将 Windows 上的网络接口“镜像”到 Linux 中，以添加新的网络功能并提高兼容性。

- ~/.wslconfig
```
[experimental]
networkingMode=mirrored
dnsTunneling=true
firewall=true
autoProxy=true
```

以下是启用此模式的当前优势：

- IPv6 支持
- 使用 localhost 地址 `127.0.0.1` 从 Linux 内部连接到 Windows 服务器。 不支持 IPv6 localhost 地址 `::1`
- 改进了 VPN 的网络兼容性
- 多播支持
- 直接从局域网 (LAN) 连接到 WSL

 备注

使用管理员权限在 PowerShell 窗口中运行以下命令，以[配置 Hyper-V 防火墙](https://learn.microsoft.com/zh-cn/windows/security/operating-system-security/network-security/windows-firewall/hyper-v-firewall)设置，从而允许入站连接：

```
Set-NetFirewallHyperVVMSetting -Name '{40E0AC32-46A5-438A-A0B2-2B479E8F2E90}' -DefaultInboundAction Allow
```
或 
```
New-NetFirewallHyperVRule -Name "MyWebServer" -DisplayName "My Web Server" -Direction Inbound -VMCreatorId '{40E0AC32-46A5-438A-A0B2-2B479E8F2E90}' -Protocol TCP -LocalPorts 80
```

这种新模式解决了使用基于 NAT（网络地址转换）的体系结构时出现的网络问题。 查找已知问题或针对 [GitHub 上的 WSL 产品存储库](https://github.com/microsoft/wsl)中发现的任何 bug 提交反馈。

## 添加入站规则
```
New-NetFirewallRule -DisplayName "WSL" -Direction Inbound  -InterfaceAlias "ethernet"  -Action Allow
```
