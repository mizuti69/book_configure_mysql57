# 性能調査

## チューニングツール
https://github.com/major/MySQLTuner-perl  
perlで動いているプログラム  
インストール  

```
# wget http://mysqltuner.pl/ -O mysqltuner.pl
# wget https://raw.githubusercontent.com/major/MySQLTuner-perl/master/basic_passwords.txt -O basic_passwords.txt
# wget https://raw.githubusercontent.com/major/MySQLTuner-perl/master/vulnerabilities.csv -O vulnerabilities.csv
```

使い方  

```
# perl mysqltuner.pl --host localhost --user root --pass mysql
```

## 性能テスト
sysbench  
https://blog.apar.jp/linux/3350/  
インストール  

```
# yum install --enablerepo=epel sysbench
```

テスト用DBとユーザー作成  

```sql
CREATE DATABASE sbtest DEFAULT CHARACTER SET utf8mb4;
GRANT ALL ON sbtest.* TO sbtest@localhost IDENTIFIED BY 'sbtest';
```

テストデータの作成  

```
# sysbench --test=oltp --db-driver=mysql --oltp-table-size=10000 --mysql-password=sbtest prepare
```

テスト実行  

```
# sysbench --test=oltp --db-driver=mysql --mysql-password=sbtest --num-threads=10 --max-requests=0 --max-time=60 --oltp-read-only=off run

sysbench 0.4.12:  multi-threaded system evaluation benchmark

Running the test with following options:
Number of threads: 10

Doing OLTP test.
Running mixed OLTP test
Using Special distribution (12 iterations,  1 pct of values are returned in 75 pct cases)
Using "BEGIN" for starting transactions
Using auto_inc on the id column
Threads started!
Time limit exceeded, exiting...
(last message repeated 9 times)
Done.

OLTP test statistics:
    queries performed:
        read:                            287042
        write:                           102089
        other:                           40866
        total:                           429997
    transactions:                        20363  (339.33 per sec.)
    deadlocks:                           140    (2.33 per sec.)
    read/write requests:                 389131 (6484.48 per sec.)
    other operations:                    40866  (680.99 per sec.)

Test execution summary:
    total time:                          60.0096s
    total number of events:              20363
    total time taken by event execution: 599.7663
    per-request statistics:
         min:                                  5.85ms
         avg:                                 29.45ms
         max:                                375.35ms
         approx.  95 percentile:              42.90ms

Threads fairness:
    events (avg/stddev):           2036.3000/35.13
    execution time (avg/stddev):   59.9766/0.01
```
