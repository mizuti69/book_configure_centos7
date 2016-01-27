# ユーザーデフォルトの設定
ユーザーを作成するときに利用する`useradd`コマンドでは引数を指定ない場合に  
デフォルトで設定されるユーザー情報があります。  

ユーザーのデフォルト設定値は下記で確認できます。  

```
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

デフォルトではユーザーID、グループIDが500番から始まるようになっています。  
初期ログインシェルや、ユーザーのデフォルトホームディレクトリを変更したい場合、  
下記ファイルを手動で編集します。  

```
# vim /etc/default/useradd
# useradd defaults file
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```
