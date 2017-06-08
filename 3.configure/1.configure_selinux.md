# SELinuxの無効化
OS7系でも今までと同じように無効化します。

現在の設定値確認  

```
# getenforce
```

設定の変更

```
# vim /etc/selinux/config
SELINUX=disabled
```

変更を反映させるために再起動します。  

```
# systemctl reboot
```
