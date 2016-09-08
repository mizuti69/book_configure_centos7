# FROM、ENVELOPE FROMの書き換え
メール送信を行う前に、FROMやENVEROPE FROMを独自ルールで自動的に書き換えることが可能。  
ローカルネットワーク内の転送用SMTPサーバから送られてくるメールのFROM書き換えなどに有用  


デフォルトではFROM、ENVELOPE FROM両方のヘッダーを書き換えます。

```
sender_canonical_classes = envelope_sender, header_sender
sender_canonical_maps = regexp:/etc/postfix/sender_canonical
```

書き換えルールの作成  

```
# vim /etc/postfix/sender_canonical
/@hogehoge.localdomain/  @localhost.localdomain
```

`@hogehoge.localdomain`FROMのメールを送信する際に`@localhost.localdomain`に書き換える  

ルールをハッシュ化  

```
# postmap /etc/postfix/sender_canocical
```

再起動して反映  

```
# postfix check
# systemctl restart postfix
```
