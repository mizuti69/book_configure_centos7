# 送信制限  
外部に送信するメールを送信先ドメインで制限する  

特定のドメイン宛てのメールは許可し、それ以外はローカルメールキューに配送（破棄）するよう設定します  

```
# vim /etc/postfix/main.cf
transport_maps = hash:/etc/postfix/transport
```


送信許可ドメインと送信許可先サーバの設定  

```
# vim /etc/postfix/transport
hogehoge.co.jp	            :hogehoge.co.jp
*                           :[127.0.0.1]
```

上記の場合`hogehoge.co.jp`宛てのメールは`hogehoge.co.jp`のMXレコード宛に送信を許可し、  
それ以外は全て`[127.0.0.1]`に送るよう設定している  

転送先をドメインにした場合、MXレコードに登録してあるIPに送信。  
[]で囲い指定した場合はAレコードに登録してあるIPへ送信。  

ルールをハッシュ化  

```
# postmap /etc/postfix/transport
```

設定の反映  

```
# systemctl restart postfix
```
