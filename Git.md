### Git

#### git 克隆与提交

* 克隆添加代码

```
git clone 地址  // github克隆代码下来
git add * // 添加修改的代码
git status // 查看状态
git commit -m ".." // 添加备注
git push // 远程推送代码
```

* 修改后提交代码

```
git pull // 每次上传代码前都要拉代码
git add * // 添加修改的代码
git status // 查看状态
git commit -m ".." // 添加备注
git push // 远程推送代码
```

#### git 分支

```
git branch // 查看分支
git branch <name> // 创建分支
git checkout <name> // 切换分支
git checkout -b <name> // 创建并切换分支
git merge <name> // 合并某分支到当前分支
git branch -d <name> // 删除某分支
```