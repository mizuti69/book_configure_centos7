# iptables
firewalldではなくiptablesを利用したい場合、デフォルトではfirewalldが有効となっているため  
iptablesを利用できるように少し操作が必要  

## firewalldの停止、無効化
同時に利用する事はできないため、firewalldを無効化します。  

```
# systemctl stop firewalld
# systemctl disable firewalld
```

## iptablesのインストール
コマンドはインストールされているが、サービスはインストールされていない。  
サービスを先にインストールする必要がある。  

```
# yum install iptables-services
```

> インストールせずにポリシーをセットし、sysconfigのファイルに登録すると  
> ポリシー管理に不整合がおきるようで？、繋がらなくなってしまうため注意する。

インストール後は今まで通りスクリプト等でポリシーの設定を管理できる。
`service iptables save`は無くなったため、ポリシーの設定はファイルに直接設定する。  

```
iptables-save > /etc/sysconfig/iptables
```
