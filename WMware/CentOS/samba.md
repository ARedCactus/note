# communite with windows11
```
yum install samba
```
```
mkdir /home/ld/folder
```

- 设置为不予许登入系统,且用户的家目录为 /home/ldd（相当于[虚拟账号](https://zhida.zhihu.com/search?q=%E8%99%9A%E6%8B%9F%E8%B4%A6%E5%8F%B7&zhida_source=entity&is_preview=1)）的ldd账号
```
useradd -d /home/ldd -s /sbin/nologin ldd
```

- 添加samba用户
```
pdbedit -a ldd
```

# experiment
## 检测系统内部是否已经安装好samba文件
```
rpm -qa | grep samba
```
### bash: rpm-qa: command not found...
```
yum install rpm
```
## 指定samba在开机启动
```
systemctl enable smb.service
```
## 配置/etc/samba/smb.conf 配置文件
```
# See smb.conf.example for a more detailed config file or
# read the smb.conf manpage.
# Run 'testparm' to verify the config is correct after
# you modified it.

[global]
	workgroup = wyu
	security = user
	netbios name=linux3122001221
	log file=/var/log/samba/smbd.log	
	log level=2
	max log size=50

	passdb backend = tdbsam


	printing = cups
	printcap name = cups
	load printers = yes
	cups options = raw

[homes]
	comment = Home Directories
	valid users = %S, %D%w%S
	browseable = No
	read only = No
	inherit acls = Yes

[printers]
	comment = All Printers
	path = /var/tmp
	printable = Yes
	create mask = 0600
	browseable = No

[print$]
	comment = Printer Drivers
	path = /var/lib/samba/drivers
	write list = @printadmin root
	force group = @printadmin
	create mask = 0664
	directory mask = 0775
[tmp]
	path=/tmp
	read only=No
	public=Yes
[share]
	read list=@share
	writable=Yes
	create mask=0664
	directory mask=0770
	path=/home/share
```
## 重启smaba服务
```
systemctl restart smb.service
```
## 新建用户mary，john 和 guest，并设置用户密码
```
useradd mary
passwd mary
```
```
useradd john
passwd john
```
```
useradd guest
passwd guest
```
## 新建组share，并且将用户mary和john加入share组中
```
groupadd share
usermod -G share mary
usermod -G share john
```
## 将mary，john，guest 加入到smbpasswd文件
```
smbpasswd -a mary
```
```
smbpasswd -a john
```
```
smbpasswd -a guest
```
## 在/home 目录下新建目录share，将其组属性改成share组
```
mkdir -p /home/share
```
```
chown :share /home/share
```
```
chmod 770 /home/share
```
## 重新启动服务
```
systemctl restart smb.service
```
## 禁用SELinux
```
getenforce
```
```
systemctl is-active firewalld.service
```
```
systemctl stop firewalld.service
```
```
systemctl disable firewalld.service
```
## 通过Linux客户端访问Linux服务器共享文件，则先在Linux的控制台上输入如下 命令查看主机172.16.99.1的共享信息
```
smbclient -L //127.0.0.1 -U mary
```
- 不行换下面
```
smbclient -L //192.168.154.128 -U mary
```
## 访问share目录，则输入如下命令
```
smbclient -c ls //127.0.0.1/share -U mary
```
## else
```
touch 1 2 3 4
```

## windows端
- win + R
```
\\127.0.0.1\share
```
## 使用smbmount命令挂载远程共享
```
mkdir -p /mnt/smb/win
```
### 将远程共享share挂载到本地 /mnt/smb/win目录
```
mount.cifs -o user=mary //172.0.0.1/share /mnt/smb/win/
```
#### 若找不到命令mount.cifs，可以通过安装套件cifs-utils解决
```
yum install cifs-utils -y
```