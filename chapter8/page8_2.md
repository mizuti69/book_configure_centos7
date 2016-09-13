# 自動アップデート設定
自動アップデートを行いたい場合は`yum-cron`をインストールします。  
デフォルトでインストールされている場合もありますが、無ければインストールします。  

```
# yum install yum-cron
```

インストールを行うと、`cron.daily`配下に`0yum-daily.cron`、  
`/etc/cron.hourly`配下に`0yum-hourly.cron`というジョブが登録され、  
日時でアップデートの確認処理が走るようになります。  
デフォルトではアップデートのインストールまで行うようになっているため、  
ここではアップデートのチェックのみを行い、メール通知するように設定します。  

**アップデートインストールの無効**  
アップデートの確認のみを行いアップデートはダウンロードを行っておきます。  

```
# vim /etc/yum/yum-cron.conf
download_updates = yes
apply_updates = no
```

**メール通知先の設定**  

```
# vim /etc/sysconfig/yum-cron
...
emit_via = email

...
email_to = root
```


**アップデートパッケージの制限**  
全てのアップデートパッケージではなく、セキュリティ関連だけにしたい場合  

```
# vim /etc/sysconfig/yum-cron
...
update_cmd = security
```

cronサービスの有効化  

```
# systemctl start yum-cron
# systemctl enable yum-cron
```