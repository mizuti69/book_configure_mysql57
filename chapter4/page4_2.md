# パラメータチューニング（サーバ用）

**tmpディレクトリ**  
デフォルトが`/var/tmp` に  

```
tmpdir = /var/tmp
```

**最大接続待ち**  
50 + (max_connections / 5)から算出  

```
back_log = 80
```

**最大接続数**  

```
max_connections = 151
```

**接続ロック**  
下記以上接続に失敗するとロックされる  

```
max_connect_errors = 100
```

**接続タイムアウト**  
`wait_timeout`がプログラム等からの接続で使われるタイムアウト、  
`interactive_timeout`は対話的、コマンド等からの接続タイムアウト  
デフォルトは両方8時間なので、プログラム用のタイムアウトは適正値にしておく。  

```
wait_timeout = 600
interactive_timeout = 28800
```


**アカウントパスワード有効期限の無効化**  
mysql57からデフォルトのパスワード有効期限が360日に設定されています。  
最新のRPMではデフォルト無効化に変更されていますが、念のため確認、定義する。  

```
default_password_lifetime = 0
```

**アカウントパスワードレベル**  
デフォルトは英数字大文字小文字数字記号を含む8文字以上となっています。  
そのくせ特殊記号を含むとパスワード認証が成功しない記号もあるため、ポリシーはLOWにしておき対応する。  

```
validate_password_policy = LOW
```

**バッファプール**  
デフォルトでは正常起動時にダンプし、起動時に読み込むようになっている  
起動時に読み込むけど量によっては時間が掛かるので、無効化してもいい気がするけど。。。  

```
innodb_buffer_pool_load_at_startup = OFF
```


**ログレベル**  
なぜか2つに分かれた。えぇ  
両方定義した場合、後に記述された設定が優先されるそうなので注意。  

| valu                                        | notes  | warnings | error |
| ------------------------------------------- | ------ | -------- | ----- |
| log_warnings = 0,log_error_verbosity = 1    | No     | No       | Yes   |
| log_warnings = 1,log_error_verbosity = 2    | No     | Yes      | Yes   |
| log_warnings >= 2,log_error_verbosity >= 3  | Yes    | Yes      | Yes   |

デフォルトは`log_error_verbosity = 3`、`log_warnings = 2`  

**ログのタイムスタンプ**  
デフォルトではUTCになっている。  
下記でシステム時刻にもなる、バイナリログは影響を受けない。  

```
log_timestamps = SYSTEM
```

**ロギング**  
システムログloggerをサポート  
デフォルトでは無効化されている。  

```
log_syslog = OFF
log_syslog_facility = daemon
```

**スロークエリログ**  

```
slow_query_log = ON
slow_query_log_file = /var/lib/mysql/%{hostname}-slow.log
long_query_time = 10.000000
```

**binlogフォーマット**  
デフォルトが変更、`MIXED`？なにそれになった。  

```
binlog_format = ROW
```

**バイナリログの保持期限**  
デフォルトは無期限  
ローテートされるタイミングは起動時、クラッシュ時  

```
expire-logs-days = 0
```

**削除されたパラメータ**  

```
binlogging_impossible_mode
innodb_additional_mem_pool_size
innodb_mirrored_log_groups
innodb_use_sys_malloc
sha256_password_private_key_path
sha256_password_public_key_path
simplified_binlog_gtid_recovery
storage_engine
thread_concurrency
timed_mutexes
```
