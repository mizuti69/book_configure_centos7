# NICの設定

OS7系よりネットワークインターフェースファイルの命名が`eth`では無くなり、  
**Predictable Network Interface Names** という新しい命名規則が採用されています。

一般的なもので下記のような命名規則があります。

| 種類 | 頭の2文字 |
| --- | --- |
| イーサネット | en |
| ワイヤレス | wl |

| 種類 | 3文字目 |
| --- | --- |
| オンボード | o |
| PCI Express | s |

Firmware/BIOSがNICの（固定的な）論理番号を提供していない場合は、  
PCI（もしくはUSB）の物理的なロケーション（バスとスロットの番号）に基づいて、  
「enp1s1」などとなります。3文字目以降が「ps」というルールになります。  
まずどのような名前でNICが登録されているのかを確認しましょう。

```
# nmcli connection show
```

NIC状態の確認

```
# nmcli device status
```

次にOSインストール時に設定しない場合デフォルトではNICが無効化されているため有効化します。

```
# nmcli con up id enoXXXXXXX
# nmcli c modify enoXXXXX connection.autoconnect yes
```

#### 固定IP設定

NICはデフォルトではDHCP設定になっているため、固定IPを割り振ります。  
ここではIPv4アドレスを設定します。

```
# nmcli con mod enoXXXXX ipv4.method manual ipv4.addr "10.96.146.XXX/20" ipv4.gateway "10.96.144.1"
```

設定の反映

```
# nmcli c up enoXXXXX
```

※アクティブなNICに対して設定変更を反映する方法としてこの方法が正しいかは要検証

#### DHCP設定

デフォルトDHCP設定ですが、コマンドからDHCP設定を行う場合。

```
# nmcli c mod enoXXXXX ipv4.method auto -ipv4.address "" -ipv4.gateway ""
```

設定の反映

```
# nmcli c up enoXXXXX
```

※アクティブなNICに対して設定変更を反映する方法としてこの方法が正しいかは要検証



NICに設定できる詳細なパラメータは下記コマンドで確認する事が出来ます。  

```
nmcli -p con show "enoXXXXX"
```



