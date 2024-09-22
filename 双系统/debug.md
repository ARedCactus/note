# 时钟不同步问题
## windows/linux处理时间和时区:
- windows:
	直接将cmos时间认定为当前显示时间（本地时间），也不会去做时区的转换。这样如果调整系统时区的话，根据时区计算时间之后也会修改CMOS时间，设置保存之后，cmos的时间就被改变了，这是表示硬件上的时间被修改了。
- linux:
	以当前的住吧你的时间作为伦敦时间（零时区），再根据系统设置的时区来最终确定当前系统时间。
## 解决方法
- 推荐在ubuntu下进行操作，也就是让ubuntu按照win的方式管理时间，禁止使用世界协调时间。
```
sudo apt-get install ntpdate                  //  在ubuntu下更新本地时间
sudo ntpdate time.windows.com           
sudo hwclock --localtime --systohc       //将本地时间更新到硬件上
```
