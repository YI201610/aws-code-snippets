# Amazon Linuxでrootになる

$ sudo su -

# yum で各種パッケージをupdate

$ yum update -y

# サーバーにmysqlとwhoisコマンドをインストール

$ yum install -y jwhois mysql

# サーバーに、php7をインストール（yumがApache2.4もインストールする）

$ yum install -y php72 php72-mbstring php72-mysqlnd

# サーバーを起動した際に、Apacheが自動で起動するようにする

$ chkconfig --add httpd
$ chkconfig httpd on

# httpdの自動設定を確認する

$ chkconfig --list httpd


```
[root@ip-xxx-xx-xx-xx ~]# chkconfig --list httpd
httpd          	0:off	1:off	2:on	3:on	4:on	5:on	6:off
```

現状のランレベルは、3なので、3のところが on になっていればOK

# サーバーのタイムゾーンを日本時間にする

$ vi /etc/sysconfig/clock

```
ZONE="Asia/Tokyo"
UTC=true
```

# シンボリックリンクを作成

$ ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# 言語設定を日本語に変更

$ vi /etc/sysconfig/i18

```
LANG=ja_JP.UTF-8
```

# Linuxを復元した際に、言語設定が戻らないようにする

$ vi /etc/cloud/cloud.cfg

次の行を追加

```
locale: ja_JP.UTF-8
```

# historyが2000件まで保存されるようにする

$ vi /etc/bashrc

末尾行に次の2行を追加

```
HISTTIMEFORMAT='%F %T '
HISTFILESIZE=2000
```

$ Amazon Linuxを再起動

$ reboot


