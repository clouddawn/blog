# git 本地仓库

## git 的6行配置

```
git config --global user.name 你的英文名
git config --global user.email 你的邮箱
git config --global push.default simple
git config --global core.quotepath false
git config --global core.editor "code --wait"
git config --global core.autocrlf input
```

* git init
  * 初始化

* git add 路径
  * git .
    * . 表示当前目录

* git commit -m 字符串
  * 提交，并说明提交理由
  * 字符串里如果有空格，就要用引号包起来

* git commit -v
  * 使用vscode写提交理由
  * 需要保证code是可以直接在命令行执行的，如果不能，需要安装vscode并配置PATH
  * 如：C:\vscode\Microsoft VS Code\bin

* .gitignore
  * 描述哪些变动是不需要提交的

* git log
  * 查看提交历史
  * 使用**q**退出

* git reset --hard xxxxxxx

  * 切换版本

  * xxx 是提交好的前7位
  * 请一定要确保已经把所有的代码 commit 了，因为这个操作会使没有 commit 过的变动消失

* git reflog
  * 查看所有提交历史
  * git log 只会显示这个版本之前的提交

* git branch x
  * 基于当前 commit 创建一个新的时间线 (分支)
  * 在哪个分支提交，代码就出现在哪个分支

* git checkou x
  * 切换分支
  * 当前目录有未提交的代码，只要跟另一个分支不冲突，就不需要理会
  * 如果冲突了，可以使用通灵术 git stash ，也可以合并冲突。

* git merge x
  * 将另一个分支合并到当前分支

* 解决冲突的办法

  * 发现冲突
    * 合并分支的时候，会得到 conflict 提示
    * 使用 git status -sb 查看哪些文件冲突了

  * 解决冲突
    * 依次打开每个文件
    * 搜索 ==== 四个等于号
    * 在上下两个部分中选择要保留的代码
    * 可以只选上面，也可以只选下面，甚至可以都选
    * 删除不用的代码，删除 ==== >>>> <<<< 这些标记
    * git add 对应文件
    * 在此 git status -sb, 解决下一个文件的冲突
    * 知道没有冲突，运行 git commit (注意不要选项)

* git branch -d x

  * 合并完后删除无用的分支 git branch -d x

    