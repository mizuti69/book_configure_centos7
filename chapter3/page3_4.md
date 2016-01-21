# システムロケール
システム全体にわたるロケール設定は /etc/locale.conf ファイルに保存され、  
systemd デーモンが初期ブート時に読み込みます。  
/etc/locale.conf で設定されたロケール設定は、個別のプログラムやユーザーが上書きしない限り、
すべてのサービスやユーザーに継承されます。  

現在のロケール確認  

```
# localectl status
```

デフォルトロケールの変更  

```
# localectl set-locale LANG=ja_JP.utf8
```
