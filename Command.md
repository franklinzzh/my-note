## Command 

### - Mac Command

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

```bash
# show all files
ls   # On macOS/Linux
sudo mkdir 
sudo mv

cat /file
sudo nano /file

tar -xzf + `file-name`.tar.gz // extract a .tar.gz file

#show command history
history

whoami

echo $0


```



### - Environment Variables 

```
nano ~/.zshrc // edit the file

Ctrl + O(Big O) // save, press Enter
Ctrl + X // quit

source ~/.zshrc // let update works

mvn -v // tes 
java -v
```



### - Docker Command

| **命令**       | **说明**                       | **文档地址**                                                 |
| :------------- | :----------------------------- | :----------------------------------------------------------- |
| docker pull    | 拉取镜像                       | [docker pull](https://docs.docker.com/engine/reference/commandline/pull/) |
| docker push    | 推送镜像到DockerRegistry       | [docker push](https://docs.docker.com/engine/reference/commandline/push/) |
| docker images  | 查看本地镜像                   | [docker images](https://docs.docker.com/engine/reference/commandline/images/) |
| docker rmi     | 删除本地镜像                   | [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) |
| docker run     | 创建并运行容器（不能重复创建） | [docker run](https://docs.docker.com/engine/reference/commandline/run/) |
| docker stop    | 停止指定容器                   | [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) |
| docker start   | 启动指定容器                   | [docker start](https://docs.docker.com/engine/reference/commandline/start/) |
| docker restart | 重新启动容器                   | [docker restart](https://docs.docker.com/engine/reference/commandline/restart/) |
| docker rm      | 删除指定容器                   | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/rm/) |
| docker ps      | 查看容器                       | [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) |
| docker logs    | 查看容器运行日志               | [docker logs](https://docs.docker.com/engine/reference/commandline/logs/) |
| docker exec    | 进入容器                       | [docker exec](https://docs.docker.com/engine/reference/commandline/exec/) |
| docker save    | 保存镜像到本地压缩文件         | [docker save](https://docs.docker.com/engine/reference/commandline/save/) |
| docker load    | 加载本地压缩文件到镜像         | [docker load](https://docs.docker.com/engine/reference/commandline/load/) |
| docker inspect | 查看容器详细信息               | [docker inspect](https://docs.docker.com/engine/reference/commandline/inspect/) |



示例：

> 安装MySQL 8.0

```bash
docker pull mysql:8.0

#set up MySQL container
docker run -d \
  --name mysql8 \
  -p 3307:3306 \
  -e MYSQL_ROOT_PASSWORD=password \
  -e TZ=Asia/Shanghai \
  mysql:8.0
docker ps

# connect to MySQL
docker exec -it mysql8 mysql -u root -p
# OR
mysql -h 127.0.0.1 -P 3307 -u root -p

# Then, update application.yml on db url
```



##### 自定义镜像



**DockerFile**

> A Dockerfile is a script that tells Docker how to build a container image.

**Command**

| **指令**       | **说明**                                     | **示例**                     |
| :------------- | :------------------------------------------- | :--------------------------- |
| **FROM**       | 指定基础镜像                                 | `FROM centos:7`              |
| **ENV**        | 设置环境变量，可在后面指令使用               | `ENV key value`              |
| **COPY**       | 拷贝本地文件到镜像的指定目录                 | `COPY ./xx.jar /tmp/app.jar` |
| **RUN**        | 执行Linux的shell命令，一般是安装过程的命令   | `RUN yum install gcc`        |
| **EXPOSE**     | 指定容器运行时监听的端口，是给镜像使用者看的 | EXPOSE 8080                  |
| **ENTRYPOINT** | 镜像中应用的启动命令，容器运行时调用         | ENTRYPOINT java -jar xx.jar  |









### - Github

##### Github无法访问

* **编辑 `hosts` 文件**

```
cat /etc/hosts //read file
sudo nano /etc/hosts //edit it

//文件末尾添加
199.232.28.133 raw.githubusercontent.com //IP could be old, if not updated concurrently
```

* 按 `Ctrl + O` 保存文件。

* 按 `Ctrl + X` 退出编辑器。
* 刷新缓存

```
sudo dscacheutil -flushcache
sudo killall -HUP mDNSResponder

ping raw.githubusercontent.com
```



##### Update Repository Name

When using `SSH keys` , remember to use `git@github.com:`

```
git remote -v // check current remote URL
git remote set-url origin git@github.com:franklin-zzh/XXXXXX.git //Updated with the new project name
git remote -v
```



### - Git command

##### Git Setup

>  `sudo` at the beginning to execute it with **administrator** privileges

```
sudo brew install git
```

##### Basic grammar

```
git log --oneline -5 // show last 5 commit log
```



##### Github Setup

> https://blog.csdn.net/weixin_42280089/article/details/88937175
>
> ```dash
> /my-project/
> ├── .git/           # Git 仓库所在
> ├── src/            # 项目的源代码
> ├── README.md       # 项目文档
> └── .gitignore      # Git 忽略文件
> ```

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

##### File synchronism:

Clone from an existing project

```bash
git clone https://franklinzzh@github.com/franklinzzh/web-ai.git
git clone https://github.com/franklinzzh/web-ai.git
```

In Github repository, clone with ` HTTPS` or `SSH`

```bash
git init
git remote add origin https://github.com/franklin-zzh/my_web.git
git remote set-url origin git@github.com:franklin-zzh/my_web.git
git remote set-url origin https://franklinzzh@github.com/franklin-zzh/my_web.git
# for personal
vim ~/.ssh/config
vim ~/.ssh/id_personal.pub
git remote set-url origin git@github-personal:franklin-zzh/my_web.git 

git pull origin main
git add . //add后面跟"."表明添加所有文件，如果只需要添加个别文件直接后面跟文件名，也可后面跟多个文件名
git commit -m "first submit" //注释说明，每次提交新文件或更改的文件都需要添加注释
git push -u origin main //将add的文件push到github仓库中去     --force
```



##### RM cache

> Can be used to remove remote repo, by delete local cache.

```bash
git rm --cached Dockerfile 
# remove a file package
git rm -r --cached app-backend
```



##### Check top-level 	

```bash
git rev-parse --show-toplevel 
ls -a | grep .git // show .git under this folder
sudo rm -rf .git //remove .git if you have a nested git repo
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
git push -u origin local-branch // Upload a local branch for the first time
```

##### Tracking branch

Connecting branches to each other

```
git branch --track new-branch origin/base-branch
git checkout --track origin/base-branch
```

##### Delete branch

```
git branch -d branch-name // can't delete the current HEAD branch
git push origin --delete branch_name // remove remote branch
```

##### Comparing branch

```
git log main..test // shows commits in test, but not in main branch
git log origin/main..main //show commits in local mian, but not in origin main branch
```



##### Typical workflow

```bash
# Morning - Sync your local repo with the team
git checkout main
git pull origin main
# Merge main into test before doing new work
git checkout test
git checkout -b test // start something new
git merge main


# During the day - develop and commit locally
# edit code files, fix bugs, write features
git add .
git commit -m "Day 0 commit"


#End of the day - prepare to upload / sync
# Merge test back into main when done
git checkout main
git pull origin main 
git checkout test
git merge test
git push origin main
```



##### Branch Switch based on Commits

When you switch between branches such as `main` and `test`, Git swaps the file contents to match the commit versions associated with each branch. For example, if you switch from `test` to `main`, any recent changes you made to `Command.md` on the `test` branch won’t appear in the `main` branch.

##### Holding two GitHub accounts

`Personal` & `Work`

```bash
# Generate two SSH keys
ssh-keygen -t ed25519 -C "personal@outlook.com" -f ~/.ssh/id_personal
ssh-keygen -t ed25519 -C "work@gmail.com" -f ~/.ssh/id_work

# Used to change passphrase
ssh-keygen -p -f ~/.ssh/id_personal

#open id_rsa file
vim ~/.ssh/id_personal.pub //this is the public one

# Add SSH config to auto-switch accounts
nano ~/.ssh/config
```

```bash
# Personal GitHub
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_personal

# Work GitHub
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_work
```

```bash
# Go to local repo
# the repo name is the same as github repo's name
git remote -v # check for repo name

# Add url if no remote
git remote add origin git@github-personal:franklinzzh/web-ai-project.git
# use set-url to change the link
git remote set-url origin git@github-personal:franklinzzh/repo.git
git remote set-url origin git@github-work:franklin-zzh/repo.git

# set Per-repository identity
git config user.name "Your Name"
git config user.email "personal@example.com"

```





### - MySQL

##### Set up

```bash
cd usr/local/mysql 

nano ~/.zshrc
export PATH="/usr/local/mysql/bin:$PATH"
source ~/.zshrc
which mysql

mysql --version
mysql -u root -p
```



##### 自启动

```
which mysqld
ls /Library/LaunchDaemons/com.mysql.mysql.plist //检查是否存在
sudo nano /Library/LaunchDaemons/com.mysql.mysqld.plist //不存在创建
```

//XML内容

```xml
<?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
      <plist version="1.0">
      <dict>
      <key>Label</key>
      <string>com.mysql.mysqld</string>
      <key>ProgramArguments</key>
        <array>
        <string>/usr/local/mysql/bin/mysqld_safe</string>
        <string>--user=mysql</string>
        </array>
      <key>RunAtLoad</key>
        <true/>
      <key>KeepAlive</key>
        <true/>
      <key>WorkingDirectory</key>
      <string>/usr/local/mysql</string>
      </dict>
    </plist>
```

```bash
sudo chown root:wheel /Library/LaunchDaemons/com.mysql.mysqld.plist
sudo launchctl load -w /Library/LaunchDaemons/com.mysql.mysqld.plist //加载服务并设置权限
sudo launchctl list | grep mysql //验证是否生效
mysql -u root -p -e "STATUS;" //重启 Mac 后检查 MySQL 是否自动运行：
```



```bash
sudo /usr/local/mysql/support-files/mysql.server start

```





### - Java & IntelliJ IDE

##### IntelliJ Command

| 模板      | 用途               |
| --------- | ------------------ |
| `sout`    | System.out.println |
| `psvm`    | main 方法          |
| `fori`    | for 循环           |
| `iter`    | foreach            |
| `ifn`     | if (var == null)   |
| `NotNull` | @NotNull 注解      |

配置企业级注释模版

```
open ~/Library/Application\ Support/JetBrains/IdeaIC2025.2/templates
```



##### Java Setup

```
touch ~/.zshrc
open -e ~/.zshrc

//write in .zshrc
# === Java JDK ===
export JAVA_HOME="/Users/franklin/Desktop/NO_Drive/tools/Java/jdk-21.0.9.jdk/Contents/Home" 
export PATH=$JAVA_HOME/bin:$PATH

java -version
javac -version
```

##### Maven Setup

* 解压 `.zip` 包

* `maven-x.x.x/conf/setting.xml` 修改配置文件

  * 改 `local- repository` 地址
  * 改私服mirror

  ```
    <mirrors>
      <mirror>
        <id>internal-repository</id>
        <name>Maven Repository Manager running on repo.mycompany.com</name>
        <url>http://repo.mycompany.com/proxy</url>
        <mirrorOf>*</mirrorOf>
      </mirror>
    </mirrors>
  ```

* 配置环境变量

  ```
  nano ~/.zshrc
  # Maven environment variables
  export M2_HOME=/Users/franklin/Desktop/NO_Drive/tools/Maven/apache-maven-3.9.11
  export PATH=$M2_HOME/bin:$PATH
  source ~/.zshrc
  
  mvn -v // 验证
  ```

##### Idea中配置Maven(全局)

打开 `All Settings` （因为做全局配置，不要再项目中打开）

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251110125101607.png" alt="image-20251110125101607" style="zoom:40%;" />

* `Build, Execution, Deployment` 中选择 `Maven` 

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251110124715486.png" alt="image-20251110124715486" style="zoom:50%;" />

* `Maven-Runner` 选择JRE版本 21
* `Build, Execution, Deployment` 的 `Compiler-Java compiler`选择 `Porject bytetype version = 21`

新建project

选择project JDK版本

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251110125846858.png" alt="image-20251110125846858" style="zoom:50%;" />

最后新建module（模块）来控制不同层



