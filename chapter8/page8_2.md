# 自動アップデート設定
自動アップデートを行いたい場合は`yum-cron`をインストールします。  
OS7系ではデフォルトでインストールされています。  

```
# yum install yum-cron
```

インストールを行うと、`cron.daily`配下に`0yum.cron`というジョブが登録され、  
日時でアップデートの確認処理が走るようになります。  
デフォルトではアップデートのインストールまで行うようになっているため、  
ここではアップデートのチェックのみを行い、メール通知するように設定します。  

**アップデートインストールの無効**  
アップデートの確認のみを行いアップデートはダウンロードを行っておきます。  

```
# vim /etc/sysconfig/yum-cron
CHECK_ONLY=yes
DOWNLOAD_ONLY=yes
```

**メール通知先の設定**  

```
# vim /etc/sysconfig/yum-cron
MAILTO=root
```

設定が終わったらジョブを実行するよう有効化しておきます。（デーモンではありません)  

```
# chkconfig yum-cron on
# service yum-cron start
```
