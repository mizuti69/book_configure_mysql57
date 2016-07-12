# リポジトリの追加
Redhat/CentOS標準のリポジトリでは古いバージョンのパッケージしかインストールされないため、  
新しいバージョンのパッケージをインストールできるようリポジトリを追加します。  

```
# wget http://dl.iuscommunity.org/pub/ius/stable/CentOS/6/x86_64/ius-release-1.0-13.ius.centos6.noarch.rpm
# wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
# rpm -ivh ius-release-1.0-13.ius.centos6.noarch.rpm epel-release-6-8.noarch.rpm
# yum-config-manager --disable ius
# yum-config-manager --disable epel
```
