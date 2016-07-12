# Mysql接続環境の設定

作業を行なう前に
mysql56以降からmysql接続ユーザーのパスワードをコマンドラインで渡すと下記のようにメッセージされます。  

```
mysql: [Warning] Using a password on the command line interface can be insecure.  
```

コマンドでのパスワード入力はセキュアではないと起こられるのでユーザー定義を行ないます。  
例えばmysqlのrootを利用するのはOSのrootアカウントからとし、定義します。  

```
# mysql_config_editor set --login-path=root --user=root --password
Enter password:
```

接続情報が下記のようにmysqlに登録され、  
定義したOSユーザーのローカルに認証用のファイルが作成されます。  

```
# mysql_config_editor print --all
[root]
user = root
password = *****
```

```
# ls -l ~/.mylogin.cnf
-rw------- 1 root root 100  5月 17 21:46 2016 /root/.mylogin.cnf
```

登録されたユーザでログインする場合下記のようにコマンド引数に渡すことでパスワード入力なく、  
またメッセージも解消されてログインできます。  

```
# mysql --login-path=root
```
