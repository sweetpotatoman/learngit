# learngit

# Git 笔记
**分布式版本控制与集中式版本控制的最大区别**  
> 集中式的版本控制，本地没有历史记录，完整的仓库只存在服务器上，如果服务器挂了就全都挂了，而分布式如果 github 挂了可以重建一个服务器，然后把任何一个人的仓库 clone 过去。`一句话总结：分布式版本控制的每个节点都是完整仓库`

### 安装 Git
---
* [Git 下载地址](https://git-for-windows.github.io/ )
* [Git User Manual](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/user-manual.html)
* [Git 中文手册](https://git-scm.com/book/zh/v2)

下载并安装Git,安装完成后，还需要最后一步设置  
`Git Bash` 命令行输入：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

### 创建版本库并创建文件上传
---
1. 创建一个空目录
    ```cmd
    mkdir learngit
    cd learngit
    ```

2. git init 将目录变成 git 仓库目录
    ```cmd
    git init
    ```

3. 把文件添加到暂存区
    ```cmd
        echo "# learngit" >> README.md
        git add README.md
    ```

4. 把文件提交到版本库
    ```cmd
    git commit -m "first commit"
    ```
    - git commit
        > -m 后面是本次提交的说明,一次可以提交多个文件  
        **注意: **`git commit` 指定文件的时候会直接提交**工作区**的文件,不指 文件   的时候 提交的是**缓存区 `stage` 的所有文件**
        
        ```
        git commit readme.txt -m "balabala"
        ```
5. example
    ```
    cat>readme.txt<<EOF
    Git is a version control system.
    Git is free software. 
    EOF
    git add readme.txt
    git commit -m "wrote a readme file"
    ```

### 时光穿梭机
---
#### 版本回退

```
git reset --hard commit_id
```

* `HEAD` 指向的版本就是当前版本，因此，Git 允许我们在版本的历史之间穿梭，使用命令 `git reset --hard commit_id`
    * Git的 `commit_d` (版本号)是一个十六进制的用 SHA1 计算出来的数字
    * 在 Git 中用 `HEAD` 表示当前版本，上一个版本就是 `HEAD^`，上一百个版本写成 `HEAD~100` 
    * 使用 `git reset --hard HEAD^` 命令退回上一个版本
* 穿梭前，用 `git log` 可以查看提交历史，以便确定要回退到哪个版本
    * 使用 `git log --pretty=oneline` 让记录单行显示
    * 使用 `git log` 或 `git reflog` 加 `file_name` 查看指定文件的历史
* 要重返未来，用 `git reflog` 查看命令历史，以便确定要回到未来的哪个版本
    * Git 提供一个命令 `git reflog` 来记录你的每一次命令,这样就可以找到所有版本的 `commit id`  

#### 工作区和暂存区
* **工作区(Working Directory)**  
你在电脑里能看到的目录
* **版本库(Repository)**  
工作区有一个隐藏目录 `.git`，这个不算工作区,而是 Git 的版本库.我们可以称它为 *Repo*  
*Repo* 里存放了很多东西,其中最重要的就是暂存区 `stage` (或者叫 index ),还有 Git 为我们自动创建的第一个分支 (`Branch`) `master`；以及指向 `master` 的一个指针叫 `HEAD`   
![repo.png](img/repo.png)  

- 前面讲了我们把文件往 `Git` 版本库里添加的时候，是分两步执行的：  
    - 第一步是用 `git add` 把文件添加进去，实际上就是把文件修改添加到**暂存区**；  
    - 第二步是用 `git commit` 提交更改，实际上就是把暂存区的所有内容**提交到当前分支**。  

#### 查看修改内容
下面是关于 `git diff`的一些使用区别  
![git_diff.png](img/git_diff.png)  
另外可以使用`git diff commit_id_1 commit_id_2`比较两个不同版本的区别  

`cat file_name`命令，其功能是显示在工作区、暂存区和分支里同名文档的**最新修改版本的内容**


### 撤销修改
* **场景1**：当你改乱了**工作区**某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file_name`
    * 可以用`git checkout -- *`丢弃所有工作区文件的修改
* **场景2**：当你不但改乱了工作区某个文件的内容，还添加到了**暂存区**时，想丢弃修改，分两步
    * 第一步用命令`git reset HEAD file_name`就回到了**场景1**
        * 使用`git reset HEAD`丢弃所有暂存区的修改
    * 第二步按**场景1**操作
* **场景3**：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考**版本回退**一节，不过前提是没有推送到远程库。

注意:使用版本退回操作`git reset --hard `会导致所有暂存区和工作区的当前修改但未commit的内容全部丢弃.
特别:使用`git reset --hard HEAD`会导致上述结果,并在`git reflog`中生成记录,但不改变









git remote add origin git@github.com:sweetpotatoman/learngit.git
git push -u origin master

