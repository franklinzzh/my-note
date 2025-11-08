## Command 

### Mac Command

| **Function**               | **Hotkey (macOS)**                                         |
| -------------------------- | ---------------------------------------------------------- |
| Cut + Paste                | Command + C / Command + Option + V                         |
| ScreenShoot(Save to local) | `Shift-Command-3` `Shift-Command-4` `Shift-Command-5`      |
| ScreenShoot(paste)         | `Shift-Option-Command-3`  3(full-screen) 4(portion) 5(app) |
| Go to a file path          | Finder `Command + Shift + G`                               |

| Symbol            | Meaning                                    |
| ----------------- | ------------------------------------------ |
| `/Users/franklin` | Starts from the **root** of the filesystem |
| `Users/franklin`  | Starts from your **current directory**     |
| `~/Desktop`       | Starts from your **home directory**        |
| `cd /`            | Go to system **root**                      |
| `pwd`             | **P**rint **W**orking **D**irectory        |
| ls -al ~/.ssh     | show all files                             |



### - Typera Command

| **Function**   | **Hotkey (macOS)**   |
| -------------- | -------------------- |
| Table          | Command + Option + T |
| Code Fence     | Command + Option + C |
| Math Block     | Command + Option + B |
| Quote          | Command + Option + Q |
| Unordered List | Command + Option + U |
| Ordered List   | Command + Option + O |
| HyperText      | Command + K          |

[Short-Cut Keys](https://support.typora.io/Shortcut-Keys/#change-shortcut-keys)



### - Terminal Command

```
# show all files
ls   # On macOS/Linux

```



### - Github无法访问

* **编辑 `hosts` 文件**

```
sudo nano /etc/hosts

//文件末尾添加
199.232.28.133 raw.githubusercontent.com
```

* 按 `Ctrl + O` 保存文件。

* 按 `Ctrl + X` 退出编辑器。
* 刷新缓存

```
sudo killall -HUP mDNSResponder
ping raw.githubusercontent.com
```





### - Git command

>  `sudo` at the beginning to execute it with **administrator** privileges

```
sudo brew install git
```

##### Basic grammar

```
git log --oneline -5 // show last 5 commit log
```



##### SetUp Git repository

> https://blog.csdn.net/weixin_42280089/article/details/88937175
>
> /my-project/
> ├── .git/           # Git 仓库所在
> ├── src/            # 项目的源代码
> ├── README.md       # 项目文档
> └── .gitignore      # Git 忽略文件

* Create github repository 

* Set name and email

  * email must match GitHub email address
  * `global` used to make sure all repository on my comp could use this name & email to track `commit` ...

  ```
  git config --global user.name "xxxx"
  git config --global user.email "xxxx@xx.com"
  ```

* SSH key (Set up everytime for different computer)

  ```
  #change passphrase for ssh
  ssh-keygen -p -f ~/.ssh/id_rsa
  #open id_rsa file
  vim ~/.ssh/id_rsa.pub
  ```

  * copy it & go to github to set up `New SSH Key`

  ```
  #test connection with github
  git remote -v
  ssh -T git@github.com
  ```

  * File synchronism: In Github repository, clone with HTTPS

  ```
  git init
  git remote add origin https://github.com/franklin-zzh/my_web.git //https 添加远程连接地址
  git remote set-url origin git@github.com:franklin-zzh/my_web.git //ssh
  git pull origin master
  git add . //add后面跟"."表明添加所有文件，如果只需要添加个别文件直接后面跟文件名，也可后面跟多个文件名
  git commit -m "first submit" //注释说明，每次提交新文件或更改的文件都需要添加注释
  git push -u origin master //将add的文件push到github仓库中去     --force
  ```

##### Push & Pull

```
git pull
git push
git branch -v
git branch -vv
```

##### Check Branch

```
git branch // check current branch
git branch test //create test branch
git checkout(switch) test //switch to test branch
git branch -m <HEAD-new-name> //change current head branch name
git branch -m <old-name> <new-name> //non-head branch

```

##### Merge branch

```
git switch main // merge always merge to the HEAD branch
git merge test // the branch need to merge
//have merge commit when two branch both have unique commits
git push
```

###### Merge & Rebase diff

> `Before` rebase:
>
> A --- B --- C (main)
>        \
>         D --- E (feature)
>
> `After` rebase:
>
> A --- B --- C --- D′ --- E′ (test) // Since add a new `C` after `B`

| Concept                        | Rebase  | Merge |
| ------------------------------ | ------- | ----- |
| Changes commit IDs             | Yes     | No    |
| Safe for shared branches       | No      | Yes   |
| Requires force push            | Usually | No    |
| Others can “pull again” safely | No      | Yes   |

Normally, when others use the same repository, don't use `rebase`, `merge` is a safer way to commit to main.

##### Publish branch

```
git push -u origin <local-branch> // Upload a local branch for the first time
```

##### Tracking branch

Connecting branches to each other

```
git branch --track <new-branch> origin/<base-branch>
git checkout --track origin/<base-branch>
```

##### Delete branch

```
git branch -d <branch-name> // can't delete the current HEAD branch
git push origin --delete branch_name // remove remote branch
```

##### Comparing branch

```
git log main..test // shows commits in test, but not in main branch
git log origin/main..main //show commits in local mian, but not in origin main branch
```



##### Typical workflow

```
//Morning - Sync your local repo with the team
git checkout main
git pull origin main
# Merge main into test before doing new work
git checkout test
git checkout -b test // start something new
git merge main


//During the day - develop and commit locally
# edit code files, fix bugs, write features
git add .
git commit -m "Day 0 commit"


//End of the day - prepare to upload / sync
# Merge test back into main when done
git checkout main
git pull origin main 
git checkout test
git merge test
git push origin main
```



##### Branch Switch based on Commits

When you switch between branches such as `main` and `test`, Git swaps the file contents to match the commit versions associated with each branch. For example, if you switch from `test` to `main`, any recent changes you made to `Command.md` on the `test` branch won’t appear in the `main` branch.

