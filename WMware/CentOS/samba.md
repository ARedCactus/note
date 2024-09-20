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

