# SU設定
SUコマンドを利用できるユーザーを制限します。  

> 注意：sudo、suを合わせて制限利用した場合にユーザー管理状況によってはOSコントロール権限を失う恐れがあります。  
>      ユーザー管理や制限は実利用環境に基づいて制限する設計を行う。  

SUコマンドを利用できるユーザーは`wheel`グループに所属しているユーザーのみとします。  

```
# vi /etc/pam.d/su
auth           required        pam_wheel.so use_uid
```

```
# vi /etc/login.defs
SU_WHEEL_ONLY yes
```

設定後、忘れずにOS管理ユーザーは`wheel`グループに所属させます。  
