# メールサーバ用の設定

**ネットワーク関連**  
主にどこからのSMTPリクエストを受け付けるか、どのネットワークでリッスンするかを指定  
内部からのSMTPリクエストを処理し、外部に送受信する場合は`mynetworks`に信頼するネットワークを設定し、  
リスニングする`inet_interfaces`に`all`か外部通信するネットワークを設定  

```
mynetworks = 127.0.0.0/8, 192.168.100.0/24
inet_interfaces = all
inet_protocols = ipv4
```

`inet_protocols`は必要により`ipv4`だけに限定している  

**メールヘッダーの書き換え**  
外部にメールを送信する際に、ローカルNW情報が流出しないよう書き換える  

```
header_checks = regexp:/etc/postfix/header_checks
```

書き換えルールの設定  

```
# vim /etc/postfix/header_checks
/(^Received:.*) \[[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+\](.*)/ REPLACE $1$2
```
