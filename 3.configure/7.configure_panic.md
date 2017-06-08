# カーネルパニック対応
カーネルパニックが発生した場合OSを再起動させる。  

```
# vim /etc/sysctl.conf
kernel.panic = 10
```

設定の反映  

```
# sysctl -p
```
