Brew fixed

公共网络存在防火墙：开启全局模式+虚拟网卡（TUN）



```
export http_proxy="http://127.0.0.1:7890"
export https_proxy="http://127.0.0.1:7890"
export all_proxy="socks5://127.0.0.1:7890"
echo "Proxy enabled"

```

```
unset http_proxy
unset https_proxy
unset all_proxy
echo "Proxy disabled"

```

