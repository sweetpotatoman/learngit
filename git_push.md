## 避免 git push 出现 “merge branch 'master' of ...”
> 在使用 Git 的进行代码版本控制的时候，往往会发现在 log 中出现 "Merge branch 'master' of ..." 这句话，如下图所示。日志中记录的一般为开发过程中对代码的改动信息，如果出现过多例如上述描述的信息会造成日志的污染。


### 产生原因分析
当多人合作开发一个项目时，本地仓库落后于远程仓库是一个非常正常的事情

- 在进行 pull 操作的同时，其实就是 `fetch+merge` 的一个过程，我们从 remote 分支中拉取新的更新，然后再合并到本地分支中去。
    1. 如果 remote 分支超前于本地分支，并且本地分支没有任何 commit 的，直接从 remote 进行 pull 操作，默认会采用 fast-forward 模式，这种模式下，并不会产生合并节点，也就是说不会产生多余的那条 log 信息
    2. 如果本地先 commit 后再去 pull，那么此时，remote 分支和本地会分支会出现分叉，这个时候使用 pull 操作拉取更新时，就会进行分支合并，产生合并节点和 log 信息

    ```
    # fast-forword 
    A-B-D(origin/master)
         \
          C'(master)
    
    # merge
    A-B-C-E(master)
       \ /
        D(origin/master)
    ```

### 如何避免
```
git pull --rebase
```  
如果拉取不产生冲突，会直接 rebase，不会产生分支合并操作，如果有冲突则需要手动 fix 后，自行合并。

### 关于 rebase 和 merge
- 从 remote 分支拉取更新到本地时，使用 rebase。
- 当完成 bug 修复或新功能时，使用 merge 将子分支合并到主分支。
- 没有人应该 rebase 一根共享的分支。