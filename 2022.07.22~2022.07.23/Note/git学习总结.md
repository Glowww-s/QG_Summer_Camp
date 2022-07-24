# git总结

## git各个部分构成

![](https://www.runoob.com/wp-content/uploads/2015/02/git-command.jpg)

## git工作流程

![](https://www.runoob.com/wp-content/uploads/2015/02/git-process.png)

<u>**下文命令出现的括号中的内容需要自行替换**</u>

### 创建仓库

- 创建本地仓库：`git init`

- 创建远程仓库：按照Github的步骤来；

- 具体情境：
  1. 从零开发：建议先建远程仓库，再克隆
  2. 先有本地仓库：
     - 创建远程仓库
     - 关联远程仓库：`git remote add origin <远程仓库的ssh密匙>`
  3. 先有远程仓库：
     - 克隆仓库：`git clone <远程仓库的ssh密匙>`

### 创建临时分支

- 查看分支：`git branch`

- 创建分支：`git branch <name>`
- 切换分支：`git checkout <name>`或者`git switch <name>`
- 创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

### 修改新建分支的文件

### 添加文件

- 将文件添加到暂存区：`git add <文件名>`

### 提交文件

- 将暂存区版本提交到版本库：`git commit -m “...”`

### 合并分支到主分支

- 合并某分支到当前分支（fast forward合并，历史无分支）：`git merge <name>`
- 合并某分支到当前分支（普通模式合并，历史无分支）：`git merge --no-ff <name>`

### 删除临时分支

- 删除分支：`git branch -d <name>`

### 更新远程仓库

- 推送修改至远程仓库：`git push origin <本地分支名>:<远程分支名>`

## 一些其他命令

- 查看状态：`git status`

  查看远程库信息：`git remote -v`

- **丢弃修改**

  - 查看工作区和版本库的区别：`git diff HEAD -- readme.txt`
  - 丢弃工作区的修改【版本库的版本替换工作区的版本】：`git checkout -- <文件名>`
  - 丢弃暂存区的修改：`git reset HEAD <文件名>`
  - 丢弃版本库的修改：见版本回退
  - 删除文件：`git rm -r <文件名>`

- **版本回退**

  - 查看历史版本：`git log --pretty=oneline`

  - 查看操作记录【用来找到后一个版本的id】：`git reflog`
  - 切换版本：`git reset --hard HEAD^`

- **推送失败则拉取远程分支**：

  - 取远程分支与当前分支合并【直接取远程的最新版本】：git pull

    【用git fetch + git merge实现更好更安全】

  - 建立本地分支与远程分支的链接：`git branch --set-upstream-to <branch-name> origin/<branch-name>`

  - **覆盖问题：**
    1. 先将本地代码放到暂存区：`git stash`
    2. 将远程github上面的代码拉取下来：`git pull origin <远程分支名>:<本地分支名>`
    3. 将第一步暂存区的代码放回本地：`git stash pop`

- **解决冲突**

  合并分支时，分支各自有了新的提交，修改至一样重新提交即可
  
- pull报错：Please enter a commit message to explain why this merge is necessary（本次提交时已有其他人提交过代码）

  1. 键盘输入‘i’
  2. 键盘输入‘esc’
  3. 键盘输入‘:wq’
  4. 键盘输入‘enter’，提交代码成功
  
- 复制某一相同修改：

  `git cherry-pick <commit>`

## 分支管理

- master（稳定版本）
- dev（测试版本）
- bug
- feature（新功能分支）

bug 和 feature可以不推远程