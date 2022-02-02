# Laporan Praktikum UAS - Sistem Administrasi Server 
Disusun oleh :
1. Rachmad saflyi
2. alifia





Buat LXC yang terdiri dari :

- 6 instance LXC ubuntu 20.04 PHP 7.4
```
sudo lxc-create -n lxc_php7_1 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_2 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_3 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_5 -t download -- --dist ubuntu --release focal --arch amd64 -force-cache --no-validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_6 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

- 2 instance LXC debian 10 PHP 5.6
```
sudo lxc-create -n lxc_php5_1 -t download -- --dist debian --release buster --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php5_2 -t download -- --dist debian --release buster --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

- 1 instance LXC debian 10 mariadb server
```
sudo lxc-create -n lxc_mariadb -t download -- --dist debian --release buster --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

Setting autostart, dan IP setiap lxc, Berikut ini adalah list lxcnya

![A1](asset/Picture1.png)

Setting sites-available pada vm menggunakan nama kelompok5.fpsas dan symlink ke sites-enabled
```
  upstream laravel {
        least_conn;
        server lxc_php7_1.dev;
        server lxc_php7_4_laravel.dev;
        server lxc_php7_6_laravel.dev;
        server lxc_php7_2_laravel.dev;
  }
  upstream yii {
        server lxc_php7_2_yii.dev weight=2;
        server lxc_php7_1_yii.dev weight=3;
        server lxc_php7_4_yii.dev weight=4;
        server lxc_php7_5_yii.dev weight=1;
        server lxc_php7_6_yii.dev weight=6;
   }
  upstream ci {
        server lxc_php5_1.dev;
        server lxc_php5_2.dev;
  }
  upstream wp {
        ip_hash;
        server lxc_php7_3_wp.dev;
        server lxc_php7_2.dev;
        server lxc_php7_4_wp.dev;
        server lxc_php7_5_wp.dev;
  }

  server {
          listen 80;
          listen [::]:80;

          server_name kelompok5.fpsas;

          root /var/www/html;
          index index.html;

          location /app {
                  rewrite /app/?(.*)$ /$1 break;
                  #proxy_pass http://lxc_php5_1.dev;
                  proxy_pass http://ci;
          }

          location /product {
                  rewrite /product/?(.*)$ /$1 break;
                  #proxy_pass http://lxc_php7_6_yii.dev;
                  proxy_pass http://yii;
          }

          location /phpmyadmin {
                  rewrite /phpmyadmin/?(.*)$ /$1 break;
                  proxy_pass http://lxc_db_server.dev;
          }

          location / {
                  #rewrite /php7/?(.*)$ /$1 break;
                  #proxy_pass http://lxc_php7_1.dev;
                  proxy_pass http://laravel;
          }

  }

  server {
         listen 80;

         server_name news.kelompok5.fpsas;

         root /var/www/html;
         index index.html;

         location / {
                  #rewrite /php7/?(.*)$ /$1 break;
                  #proxy_pass http://lxc_php7_3_wp.dev;
                  proxy_pass http://wp;
         }
  }

```

Daftar semua lxc pada /etc/hosts di vm
```
127.0.0.1 localhost
127.0.1.1 sas01
127.0.0.1 kelompok5.fpsas news.kelompok5.fpsas

#laravel
10.0.3.101  lxc_php7_1.dev
10.0.3.102  lxc_php7_2_laravel.dev
10.0.3.104  lxc_php7_4_laravel.dev
10.0.3.106  lxc_php7_6_laravel.dev

#yii
10.0.3.102  lxc_php7_2_yii.dev
10.0.3.101  lxc_php7_1_yii.dev
10.0.3.104  lxc_php7_4_yii.dev
10.0.3.105  lxc_php7_5_yii.dev
10.0.3.106  lxc_php7_6_yii.dev

#wp
10.0.3.103  lxc_php7_3_wp.dev
10.0.3.102  lxc_php7_2.dev
10.0.3.104  lxc_php7_4_wp.dev
10.0.3.105  lxc_php7_5_wp.dev

#ci
10.0.3.111  lxc_php5_1.dev
10.0.3.112  lxc_php5_2.dev

#db
10.0.3.200  lxc_db_server.dev
#10.0.3.201  lxc_db_server_coba.dev

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

Deploy website menggunakan ansible:

Setting hosts ansible

![A1](asset/Picture2.png)

# Install Mariadb
Nano install-mariadb.yml
```
- hosts: database
  vars:
    username: 'admin'
    password: 'chintya'
    domain: 'lxc_db_server.dev'
  roles:
    - db
    - pma
```

# Roles db

![A1](asset/Picture3.png)
```
---
- name: restart mysql
  become: yes
  become_user: root
  become_method: su
  action: service name=mysql state=restarted 
```

![A1](asset/Picture4.png)
```
---
- name: delete apt chache
  become: yes
  become_user: root
  become_method: su
  command: rm -vf /var/lib/apt/lists/*

- name: install mariadb
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
   - python
   - mariadb-server
   - mariadb-client
   - python-mysqldb
   - python-pymysql

- name: Stop MySQL
  service: name=mysqld state=stopped

- name: set environment variables
  shell: systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"

- name: Start MySQL
  service: name=mysqld state=started

- name: sql query
  command:  mysql -u root --execute="UPDATE mysql.user SET authentication_string = PASSWORD('{{ password }}') WHERE User = 'root' AND Host = 'localhost';"

- name: sql query flush
  command:  mysql -u root --execute="FLUSH PRIVILEGES"

- name: Stop MySQL
  service: name=mysqld state=stopped

- name: unset environment variables
  shell: systemctl unset-environment MYSQLD_OPTS

- name: Start MySQL
  service: name=mysqld state=started

- name: Create user for mysql
  command:  mysql -u root --execute="CREATE USER IF NOT EXISTS '{{ username }}'@'localhost' IDENTIFIED BY '{{ password }}';"

- name: GRANT ALL PRIVILEGES to user {{username}}
  command:  mysql -u root --execute="GRANT ALL PRIVILEGES ON * . * TO '{{ username }}'@'localhost';"

- name: Create user for remote mysql
  command:  mysql -u root --execute="CREATE USER IF NOT EXISTS '{{ username }}'@'%' IDENTIFIED BY '{{ password }}';"

- name: GRANT ALL PRIVILEGES to remote user {{username}}
  command:  mysql -u root --execute="GRANT ALL PRIVILEGES ON * . * TO '{{ username }}'@'%';"

- name: sql query flush
  command:  mysql -u root --execute="FLUSH PRIVILEGES"

- name: Create DB Landing
  command:  mysql -u root --execute="CREATE DATABASE IF NOT EXISTS `landing`;"

- name: Create DB product
  command:  mysql -u root --execute="CREATE DATABASE IF NOT EXISTS `product`;"

- name: Create DB app
  command:  mysql -u root --execute="CREATE DATABASE IF NOT EXISTS `app`;"

- name: Create DB news
  command:  mysql -u root --execute="CREATE DATABASE IF NOT EXISTS `news`;"

- name: Copy .my.cnf file with root password credentials
  template:
    src=templates/my.cnf
    dest=/etc/mysql/mariadb.conf.d/50-server.cnf
  notify: restart mysql
```

![A1](asset/Picture5.png)
```
#
# These groups are read by MariaDB server.
# Use it for options that only the server (but not clients) should see
#
# See the examples of server my.cnf files in /usr/share/mysql

# this is read by the standalone daemon and embedded servers
[server]

# this is only for the mysqld standalone daemon
[mysqld]

#
# * Basic Settings
#
user                    = mysql
pid-file                = /run/mysqld/mysqld.pid
socket                  = /run/mysqld/mysqld.sock
port                   = 3306
basedir                 = /usr
datadir                 = /var/lib/mysql
tmpdir                  = /tmp
lc-messages-dir         = /usr/share/mysql
skip-external-locking

# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address            = 0.0.0.0

#
# * Fine Tuning
#
key_buffer_size        = 16M
max_allowed_packet     = 16M
thread_stack           = 192K
thread_cache_size      = 8
# This replaces the startup script and checks MyISAM tables if needed
# the first time they are touched
myisam_recover_options = BACKUP
#max_connections        = 100
#table_cache            = 64
#thread_concurrency     = 10

#
# * Query Cache Configuration
#
query_cache_limit      = 1M
query_cache_size        = 16M

#
# * Logging and Replication
#
# Both location gets rotated by the cronjob.
# Be aware that this log type is a performance killer.
# As of 5.1 you can enable the log at runtime!
#general_log_file       = /var/log/mysql/mysql.log
#general_log            = 1
#
# Error log - should be very few entries.
#
log_error = /var/log/mysql/error.log
#
# Enable the slow query log to see queries with especially long duration
#slow_query_log_file    = /var/log/mysql/mariadb-slow.log
#long_query_time        = 10
