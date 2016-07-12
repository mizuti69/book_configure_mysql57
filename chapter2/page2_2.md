# Mysqlのインストール
MySQLを他パッケージから入れようとする場合、  
`mysql-libs`が他パッケージと依存関係でインストールされているためそのままではインストールできません。  

すでにインストールされているmysql関連パッケージと入れたいパッケージを入れ替えられるよう  
ツールをインストールします。  

```
# yum install –enablerepo=ius,epel yum-plugin-replace
```

**mysqlユーザーの作成**  
デフォルトでは下記のようなユーザーが作成されます。  
必要により事前に任意のIDで作成しておく事もできます。

```
# id mysql
uid=27(mysql) gid=27(mysql) 所属グループ=27(mysql)

# getent passwd mysql
mysql:x:27:27:MySQL Server:/var/lib/mysql:/sbin/nologin
```

**mysqlのインストール**  

```
# yum --enablerepo=epel,ius replace mysql --replace-with mysql57u
# yum install mysql57u-server --enablerepo=ius
```

クライアントのみをインストールする場合  

```
# yum --enablerepo=epel,ius replace mysql --replace-with mysql57u
# yum install mysqlclient16 --enablerepo=ius
```

**Mysqlの起動**  
※初期状態ではデータファイルは`/var/lib/mysql`配下に作成されます。  
任意の場所に出力したい場合は先に`my.cnf`ファイルで`datadir`を指定しておきましょう。  

```
# service mysqld start
```
