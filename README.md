# Git Instruction
> [zimei11/GitInstruction: git使用说明 (github.com)](https://github.com/zimei11/GitInstruction)

[toc]

## 一、Git基本概念

*   工作区：仓库的目录。工作区是独立于各个分支的。
*   暂存区：数据暂时存放的区域，类似于工作区写入版本库前的缓存区。暂存区是独立于各个分支的。
*   版本库：存放所有已经提交到本地仓库的代码版本
*   版本结构：树结构，树中每个节点代表一个代码版本。

## 二、Git应用场景

### 新项目

#### 克隆远程仓库

```
git clone XXX //克隆代码库
```

#### 本地创建再关联

`git init`：将当前目录配置成git仓库，信息记录在隐藏的.git文件夹中

`git remote add origin git@xxx:xxx/XXX.git`：将本地仓库关联到远程仓库

### 完成修改并提交

#### 个人开发

```
进行修改

git add . //把所有修改加入暂存区
or
git add XX //将XX文件添加到暂存区

git commit -m '给自己看的备注信息' //提交修改到xxx分支

git push origin xxx//把xxx分支的代码push到远程库
```

#### 团队协作

项目应该拥有一个**被保护的主分支**，只有项目负责人可以修改主分支代码

每个开发者应该**新建一个分支**进行开发，防止污染主分支。

开发完成后可以直接push子分支，或者将主分支代码合并到子分支再push（注意**两种方案均未修改主分支代码**），等待项目负责人审查代码后，merge到主分支。

```
git checkout -b xxx //新建xxx分支
or
git checkout xxx //切换到xxx分支

进行修改

git add . //把所有修改加入暂存区
or
git add XX //将XX文件添加到暂存区

git commit -m '给自己看的备注信息' //提交修改到xxx分支

git checkout master //切换到主分支
git pull //更新代码
git checkout xxx //切换到xxx分支
git meger master //把主分支的代码merge到xxx分支

git push origin xxx//把xxx分支的代码push到远程库
```



### 回滚代码

`git reset --hard HEAD^` 或 `git reset --hard HEAD~`：将代码库回滚到上一个版本

*   `git reset --hard HEAD^^`：往上回滚两次，以此类推
*   `git reset --hard HEAD~100`：往上回滚100个版本
*   `git reset --hard 版本号`：回滚到某一特定版本



`git checkout — XX`：丢弃xx文件工作区的修改，并用最近一次的commit内容还原到当前工作区（**对文件中内容的操作，无法对添加文件、删除文件起作用**）



## 三、命令大全

1.  `git config --global user.name xxx`：设置全局用户名，信息记录在`~/.gitconfig`文件中
2.  `git config --global user.email xxx@xxx.com`：设置全局邮箱地址，信息记录在`~/.gitconfig`文件中
3.  `git init`：将当前目录配置成git仓库，信息记录在隐藏的.git文件夹中
4.  `git add XX`：将XX文件添加到暂存区
    *   `git add .`：将所有待加入暂存区的文件加入暂存区
5.  `git rm --cached XX`：将文件从仓库索引目录中删掉
6.  `git commit -m "给自己看的备注信息"`：将暂存区的内容提交到当前分支
7.  `git status`：查看仓库状态
8.  `git diff XX`：查看XX文件相对于暂存区修改了哪些内容
9.  `git log`：查看当前分支的所有版本
10.  `git reflog`：查看HEAD指针的移动历史（包括被回滚的版本）
11.  `git reset --hard HEAD^` 或 `git reset --hard HEAD~`：将代码库回滚到上一个版本
     *   `git reset --hard HEAD^^`：往上回滚两次，以此类推
     *   `git reset --hard HEAD~100`：往上回滚100个版本
     *   `git reset --hard 版本号`：回滚到某一特定版本
12.  `git checkout — XX`或`git restore XX`：将XX文件尚未加入暂存区的修改全部撤销
13.  `git remote add origin git@git.acwing.com:xxx/XXX.git`：将本地仓库关联到远程仓库
14.  `git push -u (第一次需要-u以后不需要)`：将当前分支推送到远程仓库
     *   `git push origin branch_name`：将本地的某个分支推送到远程仓库
15.  `git clone git@git.acwing.com:xxx/XXX.git`：将远程仓库XXX下载到当前目录下
16.  `git checkout -b branch_name`：创建并切换到`branch_name`这个分支
17.  `git branch`：查看所有分支和当前所处分支
18.  `git checkout branch_name`：切换到`branch_name`这个分支
19.  `git merge branch_name`：将分支`branch_name`合并到当前分支上
20.  `git branch -d branch_name`：删除本地仓库的`branch_name`分支
21.  `git branch branch_name`：创建新分支
22.  `git push --set-upstream origin branch_name`：设置本地的`branch_name`分支对应远程仓库的`branch_name`分支
23.  `git push -d origin branch_name`：删除远程仓库的`branch_name`分支
24.  `git pull`：将远程仓库的当前分支与本地仓库的当前分支合并
     *   `git pull origin branch_name`：将远程仓库的`branch_name`分支与本地仓库的当前分支合并
25.  `git branch --set-upstream-to=origin/branch_name1 branch_name2`：将远程的`branch_name1`分支与本地的`branch_name2`分支对应
26.  `git checkout -t origin/branch_name` 将远程的`branch_name`分支拉取到本地
27.  `git stash`：将工作区和暂存区中尚未提交的修改存入栈中
28.  `git stash apply`：将栈顶存储的修改恢复到当前分支，但不删除栈顶元素
29.  `git stash drop`：删除栈顶存储的修改
30.  `git stash pop`：将栈顶存储的修改恢复到当前分支，同时删除栈顶元素
31.  `git stash list`：查看栈中所有元素
