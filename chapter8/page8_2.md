# 自動アップデート設定
自動アップデートを行いたい場合は`yum-cron`をインストールします。  
OS7系ではデフォルトでインストールされています。  

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
MAILTO=root
```
