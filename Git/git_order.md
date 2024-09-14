# *generating git ssh*
## 配置用户名和邮箱信息
```
git config --global user.name “ARedCactus”
```
```
git config --global user.email “3288538388@qq.com”
```

## 生成SSH Key
```
ssh-keygen -t rsa -C "3288538388@qq.com"
```

## 添加公钥至github

## 检测是否配置成功
```
ssh -T git@github.com
```
