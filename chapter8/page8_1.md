# アップデートの適応
CentOS/Redhat にはパッケージ管理ツールとして`yum`が提供されています。
OS7系では`dnf`はまだ採用されていないため、今までどおりyumを利用する事が可能です。   
OSパッケージ全てのバージョンをアップデートする場合は下記コマンドひとつで完了します。  

```
# yum update
```

アップデート可能パッケージの確認は下記で確認できます。  

```
# yum check-update
# yum check-update パッケージ名
```

Proxy配下環境でyumを利用する場合はProxy設定をyum用に設定しておく必要があります。  

```
# vim /etc/yum.conf
proxy=http://proxy-server.com:8080/
```

yumで定期的にアップデートを適用したい場合フロントエンドで利用するApacheなどのアップデートは行いたいが、  
kernelなど動作環境やバージョンが変わっては困る物は間違ってアップデートしないよう、  
yumの処理で除外するようにしておきます。  

```
# vim /etc/yum.conf
exclude=kernel*
installonlypkgs=kernel kernel-smp kernel-devel kernel-smp-devel kernel-largesmp kernel-largesmp-devel kernel-hugemem kernel-hugemem-devel
```
