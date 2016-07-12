# その他  

**TIMESTAMP**  

```
[Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
```

タイムスタンプに関する定義がされてないよ的なエラー  
`explicit_defaults_for_timestamp = ON`にするとwarningはでなくなるが、アプリ要件な気がする。  

**SSL**  

```
[Warning] CA certificate ca.pem is self signed.
```

デフォルトではSSLが有効化されているため、SSL利用してないよーてきな。  
`ssl = OFF`でログでなくする事もできるが、そのままでも大丈夫かも  

**NAME RESOLV**  

```
[Warning] 'user' entry 'root@localhost' ignored in --skip-name-resolve mode.
```

`skip_name_resolve`指定してるけどユーザー定義にホスト名あるよ？的な  
オプションを指定しなければ出ない。  

**サンプル**  

```
#
# These groups are read by MySQL server.
# Use it for options that only the server (but not clients) should see
#
# See the examples of server my.cnf files in /usr/share/mysql/
#

# this is read by the standalone daemon and embedded servers
[server]

# this is only for the mysqld standalone daemon
# Settings user and group are ignored when systemd is used.
# If you need to run mysqld under a different user or group,
# customize your systemd unit file for mysqld/mariadb according to the
# instructions in http://fedoraproject.org/wiki/Systemd
[mysqld]

## default
port = 3306
socket = /var/lib/mysql/mysql.sock
pid-file = /var/run/mysqld/mysqld.pid
character_set_server = utf8
datadir = /var/lib/mysql
tmpdir = /var/tmp
#skip_name_resolve
explicit_defaults_for_timestamp = ON

## session
max_connections = 151
back_log = 80
max_connect_errors = 100
wait_timeout = 600
interactive_timeout = 28800
max_allowed_packet = 16M
ssl = OFF

## loging
expire_logs_days = 7

log_error = /var/log/mysqld/mysqld.log
log_error_verbosity = 3
log_timestamps = SYSTEM

slow_query_log = ON
slow_query_log_file = /var/log/mysqld/slow_query.log
long_query_time = 2


## relasion
server_id = 1


# this is only for embedded server
[embedded]
```
