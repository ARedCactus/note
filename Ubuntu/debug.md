# python——报错解决：/usr/bin/env: ‘python\r’: No such file or directory
## 异常原因：
- DOS系统下和Linux系统下对于换行键"\r"的表示不同
- 在windows下，用连续的’\r’和’\n’两个字符进行换行。‘\r’为回车符，’\n’为换行符，比如原来的’aaabbb’更改为’aaa \n bbb’后输出的结果为：aaa 换行 bbb
- #!/usr/bin/env python\r\n    在Linux下，用’\n’进行换行
- #!/usr/bin/env python\n  所以windows下的程序会认为#!/usr/bin/env python是一行，而linux会认为#!/usr/bin/env python\r是一行。
## 解决方法：
- 通过apt-get命令安装[dos2unix](https://so.csdn.net/so/search?q=dos2unix&spm=1001.2101.3001.7020)的包，然后通过dos2unix这个命令即可完成转换
```
sudo apt-get install dos2unix
dos2unix <filename>
```

