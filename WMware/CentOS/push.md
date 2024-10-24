# 从服务器172.22.0.101 获取 download脚本
```
cd /home/
```
```
wget --ftp-user=ftp --ftp-password=ftp --preserve-permissions ftp://172.22.0.101/*
```
# 下载任课教师指定的考试数据
```
./download bondrong 172.22.0.101
```
# 查看学生本人考试所需配置的IP地址（例如:172.16.21.1）
```
cd /home/course
```
```
cat linux_exam.txt | grep 3122001221
```
# 提交
```
./upload 3122001221 172.22.0.101
```
# 查询成绩
```
./getScore 3122001221 172.22.0.101
```
