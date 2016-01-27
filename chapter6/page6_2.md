# セキュリティ設定

**ROOTログインの拒否**  
初期インストール時にはROOTユーザーでのログインが許可されている場合があります。  
OSでの作業ユーザー作成、`sudo`などの設定は完了していれば速やかに無効にしておきます。  

```
# vim /etc/ssh/sshd_config
PermitRootLogin no
```

**SSH利用ユーザー・グループの制限**  
SSH接続を許可するユーザー・グループを指定することも可能です。  

```
AllowUsers ユーザー名
AllowGroups グループ名
```

また逆にブラックリストの`DenyUsers`、`DenyGroups`もあります。  
