> Git 常用命令

```
git init                      初始化仓库

git status                    查看当前状态（是否有文件未提交）

git add .                     把新增的、修改的都加到缓存
git add -A                    把新增、和修改的、和删除的都加到缓存

git commit -m '版本描述'      提交到文件库
git commit -am '版本描述'     一步完成提交

git pull                      拉取远端代码
git push                      将本地代码推送远端

git switch                    切换分支
git switch -c <branch>        切换并创建分支

git branch                    查看本地分支
git branch -r                 查看远端所有分支
git branch -a                 查看本地和远端的所有分支
git branch -d <branch>        删除分支
git branch -D <branch>        强制删除分支(当修改的分支未合并用-d事无法删除的，所以要用到强制删除)

git merge <branch>            将分支的代码合并到当前所在的分支
git merge <branch> --no-ff    推荐使用这种合并

git log                       查询提交记录
git log -2                    查看最后的2次提交 数字可以是N
git log --pretty=oneline      查询提交记录(备注与HEAD在一行显示)
git log --graph               显示ASCII图形表示的分支合并历史





```

> Git新建忽略文件  目录下建立一个.gitignore文件(可以有多个，影响范围当前文件及子文件)
```
touch .gitignore
```
.gitignore文件忽略内容demo
```
# Maven #
target/
 
# IDEA #
.idea/
*.iml
 
# Eclipse #
.settings/
.classpath
.project
```
 <font color=#ff502c>
  注意：新建的一个忽略文件，为什么没有生效 </br></br>
  答：可能是因为你的缓存区已经有忽略的文件了，所以需要先清空缓存区里的文件，重新add和commit操作
</font>
删除缓存区所有文件命令

```
git rm -r --cached .      主要这个点一定要写

git add .                 重新add到缓存区
```
