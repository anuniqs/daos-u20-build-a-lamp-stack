## U20, LAMP —( L ) Linux

`anup@lamp:/var/log$ cat /etc/os-release`

`anup@lamp:/var/log$ sudo apt-get update`

`anup@lamp:/var/log$ sudo apt-get upgrade`

`anup@lamp:/var/log$ cd /var/log/`

`anup@lamp:/var/log$ sudo multitail syslog`





## U20, LAMP —( A ) Apache

### Installation,

`anup@lamp:~$ sudo apt-get update`

`anup@lamp:~$ sudo apt-cache policy apache2`

`anup@moodle:~$ sudo apt-get install apache2`

`anup@lamp:~$ dpkg -l | grep -i "apache2"`

### Version,

`anup@lamp:~$ apache2 -v`

### Service Control,

`anup@lamp:~$ sudo systemctl status apache2.service`

`anup@lamp:~$ sudo systemctl enable apache2.service`

`anup@lamp:~$ sudo systemctl start apache2.service`

### Logs,

`anup@lamp:~$ ls -ltr /var/log/apache2/`

### Port, 80, 443, and Process

`anup@lamp:~$ sudo lsof -i -P -n | grep LISTEN`

`anup@lamp:~$ sudo netstat -tulpn | grep LISTEN`

### `anup@lamp:~$ ps -aux | grep -i "apache2"`

### Directory,

`/usr/sbin/apache2`

`/var/www/html/`

`/etc/apache2/`

### Firewall,

`anup@lamp:~$ sudo ufw status`

`anup@lamp:~$ sudo ufw enable`

`anup@lamp:~$ sudo ufw allow 80`

`anup@lamp:~$ sudo ufw allow 443`

`anup@lamp:~$ sudo ufw app list`

`anup@lamp:~$ sudo ufw status`

### Access,

`anup@lamp:~$ telnet 192.168.56.12 80`

`anup@lamp:~$ curl -Is http://192.168.56.12 | head -1`

### Open your favorite browser : [http://192.168.56.12/](http://192.168.56.12/ "http://192.168.56.12/")





## U20, LAMP —( M ) MySQL
### Installation,

`anup@lamp:~$ sudo apt-get update`

`anup@lamp:~$ sudo apt-cache policy mysql-client`

`anup@lamp:~$ sudo apt-cache policy mysql-server`

`anup@lamp:~$ sudo apt-get install mysql-client`

`anup@lamp:~$ sudo apt-get install mysql-server`

`anup@lamp:~$ dpkg -l | grep -i "mysql-client"`

`anup@lamp:~$ dpkg -l | grep -i "mysql-server"`

### Version,

`anup@lamp:~$ mysql -V`

### Service Control,

`anup@lamp:~$ sudo systemctl status mysql.service`

`anup@lamp:~$ sudo systemctl enable mysql.service`

`anup@lamp:~$ sudo systemctl start mysql.service`

### Securing the MariaDB Server,

`anup@lamp:~$ sudo mysql_secure_installation`

`1!vQxy@KczdAHh`

### Logs,

`anup@lamp:~$ ls -ltr /var/log/mysql/`

### Port, 3306, and Process

`anup@lamp:~$ sudo lsof -i -P -n | grep LISTEN`

`anup@lamp:~$ sudo netstat -tulpn | grep LISTEN`

`anup@lamp:~$ ps -aux | grep -i "mysql"`

### Directory,

`anup@lamp:~$ ls -ltr /etc/mysql/`

### Firewall,

`anup@lamp:~$ sudo ufw status`

`anup@lamp:~$ sudo ufw enable`

`anup@lamp:~$ sudo ufw allow 3306`

`anup@lamp:~$ sudo ufw app list`

`anup@lamp:~$ sudo ufw status`

### Access,

`anup@lamp:~$ sudo mysql -u root -p -h localhost` , `!vQxy@KczdAHh`

`1mysql> show databases; 2 3mysql> SELECT User, Host, plugin FROM mysql.user; 4 5mysql> CREATE DATABASE bookstore; 6`

#### Create books table,

`1mysql> use bookstore;`

`1CREATE TABLE books ( 2isbn CHAR(20) PRIMARY KEY, 3title VARCHAR(50), 4author_id INT, 5publisher_id INT, 6year_pub CHAR(4), 7description TEXT );`

`1mysql> DESCRIBE books;`

`1INSERT INTO books 2(title, author_id, isbn, year_pub) 3VALUES('The Castle', '1', '0805211063', '1998');`

`1INSERT INTO books 2(title, author_id, isbn, year_pub) 3VALUES('The Trial', '1', '0805210407', '1995'), 4('The Metamorphosis', '1', '0553213695', '1995'), 5('America', '1', '0805210644', '1995');`

`1mysql> select * from books;`

#### Create authors table,

`1CREATE TABLE authors 2(author_id INT AUTO_INCREMENT PRIMARY KEY, 3name_last VARCHAR(50), 4name_first VARCHAR(50), 5country VARCHAR(50) );`

`1mysql> DESCRIBE authors;`

`1INSERT INTO authors 2(name_last, name_first, country) 3VALUES('Kafka', 'Franz', 'Czech Republic');`

`1mysql> select * from authors;`

#### Create a user,

`anup@lamp:~$ sudo mysql -u root -p -h localhost` , `!vQxy@KczdAHh`

`1mysql> CREATE USER 'anuniqs'@'%' IDENTIFIED WITH mysql_native_password BY 'aBkJwU@@Cmc9B'; 2 3mysql> GRANT ALL ON bookstore.* TO 'anuniqs'@'%'; 4 5mysql> FLUSH PRIVILEGES; 6 7mysql> EXIT;`

`anup@lamp:~$ mysql -u anuniqs -p` , `aBkJwU@@Cmc9B`

`1mysql> show databases; 2 3mysql> use bookstore; 4 5mysql> show tables; 6 7mysql> EXIT;`






## U20, LAMP —( P ) PHP

### Installation,

`anup@lamp:~$ sudo apt-get update`

`anup@lamp:~$ sudo apt-cache policy php`

`anup@lamp:~$ sudo apt-get install php libapache2-mod-php php-mysql`

`anup@lamp:~$ dpkg -l | grep -i "php"`

### Version,

`anup@lamp:~$ php -v`

### Logs,

By default, `/var/log/apache2/error.log` , But this can be configured in `/etc/php5/apache2/php.ini`.

### Directory,

`anup@lamp:~$ ls -ltr /etc/php/7.4/`

`anup@lamp:~$ ls -ltr /etc/php/7.4/apache2/`
