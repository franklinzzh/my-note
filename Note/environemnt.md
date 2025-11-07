## Terminal 

### -Github无法访问

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





### -Git command

##### Terminal

>  `sudo` at the beginning to execute it with **administrator** privileges

```
sudo brew install git
```

