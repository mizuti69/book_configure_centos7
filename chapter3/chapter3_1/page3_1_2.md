# ホスト名の設定
ホスト名には3つのクラスがあります。  

* **static**  
  従来の hostname で、ユーザーが選択することができ、/etc/hostname ファイルに保存されます。  
* **transient**  
  hostname はカーネルによって維持される動的なホスト名です。デフォルトでは`static`ホスト名に初期化され、  
  その値は「localhost」になります。ランタイム時にDHCPまたはmDNSによる変更が可能です。  
* **pretty**  
  ユーザーに自由形式の UTF8 ホスト名を提示するものです。  

ホスト名の確認  

```
# hostnamectl status
```

ホスト名の設定  

```
# hostnamectl set-hostname ${HOST_NAME}
```

`nmcli`コマンドでもパラメータの設定を出来るが、`hostnamed`には反映されない。  
`hostname`は`hostnamed`と`NetworkManager`両方で別々に管理されているため注意が必要。  
`nmcli`で`hostname`を変更した場合`hostnamed`を再起動する必要がある。  

```
# # systemctl restart systemd-hostnamed
```

hostsには今までどおり手動で追記しておく。  
