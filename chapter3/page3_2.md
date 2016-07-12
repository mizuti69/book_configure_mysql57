# Mysqlデータベース/ユーザーの作成

利用するデータベースとデータベース用ユーザーを作成します。  


**データベースの作成**  

```sql
CREATE DATABASE データベース名 DEFAULT CHARACTER SET utf8mb4;
```

**ユーザーの作成***  

アプリデータベースの管理アカウントを作成  

```sql
GRANT ALL ON データベース名.* TO 'ユーザー名'@'localhost' IDENTIFIED BY 'パスワード';
```

リモートのみ利用するアプリケーションアカウントの作成  

```sql
GRANT SELECT,INSERT,UPDATE,DELETE ON データベース名.* TO 'ユーザー名'@'%' IDENTIFIED BY 'パスワード';
```