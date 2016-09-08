# IPv6の無効化
必要によりipv6を無効化しておきます。  

NICのipv6モジュールを無効化。  

```
# nmcli c modify enoXXXXXXX ipv6.method ignore
```

システム上ipv6モジュールを無効化。  
kernelレベルでipv6を無効化する場合、
以前はmodprobedを利用してkernelのipv6モジュール読み込みを無効化していたが、  
kernelレベルで無効化することによりSELinuxの動作異常やミドルウェアのエラーが発生する事があるため  
モジュールを読み込んだ上でパラメータを無効にする方法が推奨されています。  

kernelパラメータを変更するためsysctlにて記述します。  
sysctl設定ファイルは分散コンフィグでの管理をより明示的に行うようになっています。  
デフォルトのパラメータは`/usr/lib/sysctl.d/*`にて管理されている。

```
# /usr/lib/sysctl.d/00-system.conf
# /usr/lib/sysctl.d/50-default.conf
```

追加、変更する場合は`sysctl.conf`か`sysctl.d/<name>.conf`ファイルに記述します。  

```
# vim /etc/sysctl.conf
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
```

反映  

```
# sysctl -p
```
