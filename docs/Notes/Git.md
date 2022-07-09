# Git

[toc]

> 参考[yangxijie的文案](https://yang-xijie.github.io/LECTURE/Git/git/)

## Git的常用操作

### Git Add

```
git add <file>
git add .
```



-----



### Git Commit

```
git commit -m "<message>"
或
git commit -m "message"
```

* 如果当你觉得某次commit上去后的修改是在不行，这时可以使用__*--amend*__来进行更改：

  ```
  git commit -m "<message>" --amend
  ```



-----



###  Git Status

* 查看每个区的状态：

  ```
  git status
  ```



-----



### Git Log

* 多次_commit_之后查看日志

  ```git log```



-----



### Git Push

```
git push origin master
```

可以将master换成任何你想要推送的分支



-----



### 版本回退

* 回退到某一次的`commit`：

```git reset --hard <commit>```

* 撤销某次`commit`所作出的更改：

```git revert <commit> ```  Git帮你提交

```git revert -n <commit>  ```  -n:  --no-commit ,自己提交

* `git reset --hard HEAD~` ～表示回到前一次的版本



----



### Git进阶-命令简写

* **zshrc**

打开*terminal*

添加zsh的配置文件：

```cat ~/.zshrc```

打开配置文件：

```vim ~/.zshrc```

添加：

```
## Git
alias ga="git add "
alias gc="git commit -m "
alias gs="git status"
alias glg="git log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
## Git END
```

添加后使用命令`source ~/.zshrc`让zsh配置文件生效。

之后我们就可以用`ga .`来添加所有文件，用`gc "update xxx"`来提交，用`glg`查看简要的提交历史……你也可以添加更多的简写。



---



## 分支

### 分支操作

```
git branch --create(-c) <branch>  创建分支
git branch  查看本地分支
git switch <branch>  切换分支
开发好了新功能之后
git switch main  切换到主分支，因为我们的所有功能都要合并到一个分支上
git merge <branch>  将开发新功能的分支的内容合并（merge）到main分支上
git branch --delete(-d) <branch>  删除开发新功能的分支，因为开发好了合并进来原来的开发分支就没有用了
git checkout <branch>
git checkout -b <branch>创建一个新分支并且切换到该分支上
```



---



## .gitignore

```
touch .gitignore
vim .gitignore
输入.DS_Store
```

为什么有时候.gitignore不生效？

```
如果本地仓库文件已被跟踪，那么即使在 .gitignore 中设置了忽略，也不起作用。
```

需要运行：

`git rm -r --cached ./<file>` 来删除仓库的记录，这样就会使文件属于`Untracked`状态，`.gitignore`就会起作用了。



---



## 常用操作

`git fetch --all `  拉取最新的版本

`git merge`  将版本合并到main中

`git commit -a -m "<commit message>" `  git add 和 git commit  合体

`git checkout <branch> `  切换分支

`git checkout -b <branch>` 	创建并切换分支

`git branch -d <branch>` 删除分支（需要先`git merge <branch>`）

`git brnch -D <branch>` 强制删除分支

`git merge <branch>` 合并分支







