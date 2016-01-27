# chroot設定
SFTPなどでFTPと同じようにchrootさせたい場合があります。  
FTPのように簡単に制御することが難しいため、あまり利用する機会がないかもしれません。  

まずchrootさせたいユーザーがログインするディレクトリの上の階層がROOT権限、  
chrootユーザーで読み書きできない権限`755`である必要があります。  

```
# mkdir /home/chroot/user
```

SSHサーバの設定にchrootしたいユーザーとディレクトリを定義しておきます。  

```
# vim /etc/ssh/sshd_config
Match User sftp-user
  ChrootDirectory ~/
  ForceCommand internal-sftp
```
