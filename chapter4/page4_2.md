# パスワードポリシー
OSのパスワードポリシーを設定、強化します。  

### パスワードの最小文字数変更
パスワードの最小文字数を8文字に変更します。  

```
# vi /etc/login.defs
PASS_MIN_LEN    8
```

### 認証フローの厳格化
パスワード認証に失敗10回した場合にユーザーを120秒ロックします。  
またパスワード設定時に「英語大文字」「英語小文字」「数字」「記号」などを利用するように制限します。  

OS7系よりfprintdモジュールがなくなっています。  
またパスワード処理の`pam_cracklib.so`が`pam_pwquality.so`になっている。  
今まで`pam_cracklib.so`で指定してきたパスワード制御はコンフィグファイルで管理されています。  
オプションは今までどおり、有効、無効、桁数を指定します。  

```
# vim /etc/security/pwquality.conf
minlen = 8
dcredit = -1
ucredit = -1
lcredit = -1
```

設定後は`pwquality.conf`を読み込むようにpamモジュールを追記する。  

```
# vim /etc/pam.d/system-auth-ac
password    required      pam_pwquality.so enforce_for_root
```

```
# vim /etc/pam.d/password-auth-ac
password    required      pam_pwquality.so enforce_for_root
```

`pam_tally2.so`モジュールも`pam_faillock.so`に変わっていますが、同様に利用できます。  

```
# vim /etc/pam.d/system-auth-ac

auth        required      pam_faillock.so preauth silent audit deny=10 unlock_time=120
auth        sufficient    pam_unix.so nullok try_first_pass
auth        [default=die] pam_faillock.so preauth silent authfail audit deny=10 unlock_time=120

account     required      pam_faillock.so
```

※`account`の記述場所は注意。一番上に書く  

また今までどおり、古いパスワードの記憶設定も行います。  

```
# vim /etc/pam.d/system-auth-ac
password    sufficient    pam_unix.so sha512 shadow nullok try_first_pass use_authtok remember=1
```

>authconfig ユーティリティーを使って認証設定を修正すると、  
system-auth および password-auth の各ファイルはauthconfig ユーティリティーからの設定で上書きされます。  
これを避けるには、設定ファイルの代わりにシンボリックリンクを作成します。

#### ロック制御
ユーザーがロックされているか、ロックの解除を行います。  

ロックの確認  

```
# faillock
```

ロックの解除  

```
# faillock --user ${username} --reset
```

#### 指紋認証
デフォルトでfprintdをインストールしており、fprintdサービスを停止している場合、  
下記のようなエラーメッセージがユーザログインのたびに出力される。  

```
XXX 01 15:05:45 hostneme fprintd: ** (fprintd:26535): WARNING **: fprint init failed with error -99
XXX 01 15:05:45 hostneme systemd: fprintd.service: main process exited, code=exited, status=157/n/a
XXX 01 15:05:45 hostneme systemd: Unit fprintd.service entered failed state.
XXX 01 15:05:45 hostneme systemd: fprintd.service failed.
```

pamでfprintdモジュールが呼び出されているが、fprintdサービスが停止しているため出力される。  
クラウド環境など指紋認証デバイスを利用しないのであれば案インストールし、  
pamから認証モジュールの呼び出しをコメントアウトしておく。  

```
# yum remove fprintd
```

```
# vim /etc/pam.d/system-auth-ac
#auth        sufficient    pam_fprintd.so
```
