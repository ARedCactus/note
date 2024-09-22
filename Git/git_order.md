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
- cd ~/.ssh/
- id_rsa是私钥，id_rsa.pub是公钥
- 进入你自己的github，进入Settings->SSHand GPG keys->New SSH key
- 在Key那栏下面将id_rsa.pub粘贴进去，点击 Add SSH key按钮添加

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