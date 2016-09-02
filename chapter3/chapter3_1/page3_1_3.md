# 参照DNS設定
NetworkManager経由で設定します。  

```
# nmcli con mod test-lab ipv4.dns "8.8.8.8 8.8.4.4"
```

設定の反映  

```
# nmcli con up enoXXXXX
```

設定された各パラメータ状況を確認しておく。  

```
# nmcli c show id enoXXXXX
```
