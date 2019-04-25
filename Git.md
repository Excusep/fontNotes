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

#### git 多人协作

```
1.git push origin <branch-name>推送自己的修改；
2.若推送失败，则远程分支比你的本地更新，应先用git pull试图合并；
3.如果合并有冲突，就解决冲突，并在本地提交；
4.没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
5.如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，
  用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
```

