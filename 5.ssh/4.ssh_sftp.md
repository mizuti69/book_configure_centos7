# SFTP設定
OpenSSH-ServerにはSFTPサーバも含まれています。  
デフォルトの利用においては困ることは無いですが、FTPのようにログを出力するようにする事も可能です。  

ここではログファシリティを`AUTHPRIV`、ログレベルを`INFO`デフォルト`umask`を`002`にしています。  

```
# vim /etc/ssh/sshd_config
Subsystem       sftp    /usr/libexec/openssh/sftp-server -f AUTHPRIV -l INFO -u 002
```

またSSHは許可せず、SFTPのみ許可したい場合はユーザー・グループ単位で指定可能です。  
SFTPのみ許可設定する場合はデフォルトの`sftp-server`ではなく、`internal-sftp`を利用します。  

```
# vim /etc/ssh/sshd_config
Match User sftp-user
        ForceCommand internal-sftp -f AUTHPRIV -l INFO -u 002
```

`internal-sftp`を利用する事で、ユーザーのログインシェルを`/sbin/nologin`にする事もできます。  
