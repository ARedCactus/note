# 配置踩坑
- #ifconfig 后网卡顺序对应wmware虚拟机网络适配器顺序
-  即 网络适配器 --> ens33
-  网络适配器2  -->  ens34
- 推荐设置为 网络适配器（桥接模式（自动）） #ens33
- 网络适配器（NAT） #ens34 
## windows端配置本地环回
- ipv4:
- IP: 172.24.7.100
- 掩码: 255.255.255.0
- 默认网关: 172.24.7.1
- DNS: 172.24.7.1
## wmware虚拟网络编辑器
- VMnet0 桥接模式  环回网卡
- VMnet1 仅主机  
- VMnet2 NAT
## /etc/sysconfig/network-scripts/
- 按照前面的选择， #ens33 对应 #本地环回网卡 ，即配置文件 #ifcfg-ens33
- BOOTPROTO=static    static，静态ip，而不是dhcp，自动获取ip地
- 加上ip地址和掩码：
```
IPADDR=172.24.7.1
NETMASK=255.255.255.0
```
