# サービスの登録

自作の起動スクリプトやツールによってサービスを自動起動や停止したい場合、  
systemdサービスにユニットサービスとして登録する事で以前のchkconfig同様に行なうことが出来ます。  

**ユニットファイルの作成**  
デフォルトでは既存のユニットファイルは下記に配置されています。  

```
/usr/lib/systemd/system
```

自作のスクリプトからキックする場合はユニットファイルをディレクトリに作成します。  

```
[Unit]
Description = Tomcat-Front service
After=syslog.target network.target

[Service]
ExecStart = /opt/app/tomcat-front/bin/tomcat_front start
ExecStop = /opt/app/tomcat-front/bin/tomcat_front stop
Type = forking
SuccessExitStatus = 143

[Install]
WantedBy = multi-user.target
```

**Unit**  
nodate  

**Service**  
nodate  

**Install**  
nodate  

**サービスの登録、自動起動設定**  
ユニットファイルをsystemdに登録する事で自動起動、停止を行なえるようになります。  

サービスの登録  

```
# systemctl enable {ユニットファイル名}
```

登録すると下記のディレクトリ配下にリンクが張られます。  

```
/etc/systemd/system
```

サービスを削除する場合は  


```
# systemctl disable {ユニットファイル名}
```

サービス登録後、ユニットファイルを変更した場合の反映  

```
# systemctl daemon-reload
```
