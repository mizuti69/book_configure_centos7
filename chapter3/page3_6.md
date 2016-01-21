# Cron設定
今までと同様に設定します。  

運用上`logrotated`の処理がランダム実行される事は困るため、  
以前と同じく指定時間で実行させるためには下記設定を行います。  

### anacronの設定
まずanacronのの実行時間を変更します。  
ここでは以前と同じく5時～6時の間で実行するように変更しています。  

```
# vi /etc/anacrontab
START_HOURS_RANGE=5-6
```

### cronの設定
`cron.dayly/*`、`cron.weekly/*`、`cron.monthly/*`の実行時間を指定時間にします。  

```
# vim /etc/crontab
05 0 * * * root run-parts /etc/cron.daily
25 0 * * 0 root run-parts /etc/cron.weekly
45 0 1 * * root run-parts /etc/cron.monthly
```

`cron.houry/*`については、`cron.d/0hourly` にて実行されています。  

またcronでジョブを実行した事をanacronに伝え、anacron実行時間帯には動作しないようにします。  
下記ジョブスクリプトをそれぞれ作成します。  

```
# vi /etc/cron.daily/0anacron
#!/bin/sh
if [ ! -e /var/run/anacron.pid ]; then
    anacron -u cron.daily
fi
```

```
# vi /etc/cron.weekly/0anacron
#!/bin/sh
if [ ! -e /var/run/anacron.pid ]; then
    anacron -u cron.weekly
fi
```

```
# vi /etc/cron.monthly/0anacron
#!/bin/sh
if [ ! -e /var/run/anacron.pid ]; then
    anacron -u cron.monthly
fi
```

それぞれに実行権限をつける事を忘れずに。  

```
# chmod 755 0anacron
```

### ジョブエラーの通知先
ジョブの標準出力情報やcronの問題が発生した場合に通知するメール通知先情報を指定します。  
ここではデフォルトから変更せず、`root`ユーザーに通知するようにします。  

```
# vi /etc/crontab
MAILTO="root"
```

```
# vi /etc/anacrontab
MAILTO="root"
```

```
# vi /etc/cron.d/0hourly
MAILTO="root"
```

ジョブのデバック用に標準出力はしたいがメール通知はしたくない場合、  
下記のようにジョブを登録することで問題を回避できます。  

```
10 0 * * * sample_job >/dev/null 2>&1
```
