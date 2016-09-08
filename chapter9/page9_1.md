# Postfixのインストール
標準でインストールされている場合が多いですが、最新のパッケージをインストールします。  

```
# yum install postfix
```

他のSMTPサーヒスがインストールされていた場合、デフォルトMTAを切り替えておきます。  

```
# alternatives --config mta
1 プログラムがあり 'mta' を提供します。

  選択       コマンド
-----------------------------------------------
*+ 1           /usr/sbin/sendmail.postfix

Enter を押して現在の選択 [+] を保持するか、選択番号を入力します:
```

自動起動設定  

```
# systemctl start postfix
# systemctl enable postfix
```
