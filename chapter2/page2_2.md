# Mysqlのインストール
MySQLを他パッケージから入れようとする場合、  
`mariadb-libs`が他パッケージと依存関係となっていますが、yum経由でインストール可能です。  

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
# yum install mysql-community-serve --enablerepo=mysql57-community  
```

クライアントのみをインストールする場合  

```
# yum install mysql --enablerepo=mysql57-community
```

**Mysqlの起動**  
※初期状態ではデータファイルは`/var/lib/mysql`配下に作成されます。  
任意の場所に出力したい場合は先に`my.cnf`ファイルで`datadir`を指定しておきましょう。  

```
# systemctl start mysqld
```
