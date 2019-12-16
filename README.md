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

git remote add origin git@github.com:sweetpotatoman/learngit.git
git push -u origin master
```