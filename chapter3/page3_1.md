# ネットワーク設定
OSインストール時にスキップしたネットワークの詳細設定を行います。  
OS7系より **NetworkManager** がネットワーク関連の設定を管理し、また管理を推奨しています。  
NetworkManagerが起動していない場合起動します。  

```
# systemctl status NetworkManager
# systemctl start NetworkManager
```

ついでに自動起動するように設定  

```
# systemctl enable NetworkManager
```

ネットワークの設定は今までどおりスクリプト形式での管理もNetworkManagerと相互に動くようになっています。  
しかし実際には補助的にサポートしている程度で将来的にサポートが下がる可能性もあるため、
NetworkManagerで設定を行っていきます。  

OS7系ではNetworkManagerを利用している場合最初に起動されます  
`/etc/init.d/network`がNetworkManagerの設定や接続の改竄をチェックします。  
NetworkManagerはsysconfig設定関連を管理するプライマリアプリケーションであり、  
`/etc/init.d/network`はフォールバック、セカンダリ機能として動作します。  
