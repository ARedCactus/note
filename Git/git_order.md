# *Generating git ssh*
## 1. 配置用户名和邮箱信息
```
git config --global user.name “ARedCactus”
```
```
git config --global user.email “3288538388@qq.com”
```

## 2. 生成SSH Key
```
ssh-keygen -t rsa -C "3288538388@qq.com"
```

## 3. 添加公钥至 Github

## 4. 检测是否配置成功
```
ssh -T git@github.com
```

# Action
- 创建新分支
- *git branch [new branch name]*
-
- 切换分支
- *git checkout [branch name]*