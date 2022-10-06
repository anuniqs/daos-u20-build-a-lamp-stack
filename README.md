# U20, LAMP —( L ) Linux

`anup@lamp:/var/log$ cat /etc/os-release`

`anup@lamp:/var/log$ sudo apt-get update`

`anup@lamp:/var/log$ sudo apt-get upgrade`

`anup@lamp:/var/log$ cd /var/log/`

`anup@lamp:/var/log$ sudo multitail syslog`



# U20, LAMP —( A ) Apache

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

`anup@lamp:~$ ps -aux | grep -i "apache2"`

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



# U20, LAMP —( M ) MySQL


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

    mysql> show databases; 
    mysql> SELECT User, Host, plugin FROM mysql.user; 4 5
    mysql> CREATE DATABASE bookstore; 6`

#### Create books table,

`mysql> use bookstore;`

    CREATE TABLE books (
    isbn CHAR(20) PRIMARY KEY,
    title VARCHAR(50),
    author_id INT,
    publisher_id INT,
    year_pub CHAR(4),
    description TEXT );

   `mysql> DESCRIBE books;`

    INSERT INTO books
    (title, author_id, isbn, year_pub)
    VALUES('The Castle', '1', '0805211063', '1998');

    INSERT INTO books
    (title, author_id, isbn, year_pub)
    VALUES('The Trial', '1', '0805210407', '1995'),
    ('The Metamorphosis', '1', '0553213695', '1995'),
    ('America', '1', '0805210644', '1995');

`mysql> select * from books;`

#### Create authors table,

    CREATE TABLE authors 
    (author_id INT AUTO_INCREMENT PRIMARY KEY,
    name_last VARCHAR(50),
    name_first VARCHAR(50), 5country VARCHAR(50) );

`mysql> DESCRIBE authors;`

    INSERT INTO authors
    (name_last, name_first, country)
    VALUES('Kafka', 'Franz', 'Czech Republic');

`mysql> select * from authors;`

#### Create a user,

`anup@lamp:~$ sudo mysql -u root -p -h localhost` , `!vQxy@KczdAHh`

    mysql> CREATE USER 'anuniqs'@'%' IDENTIFIED WITH mysql_native_password BY 'aBkJwU@@Cmc9B';
    mysql> GRANT ALL ON bookstore.* TO 'anuniqs'@'%';
    mysql> FLUSH PRIVILEGES;
    mysql> EXIT;

`anup@lamp:~$ mysql -u anuniqs -p` , `aBkJwU@@Cmc9B`

    mysql> show databases;
    mysql> use bookstore;
    mysql> show tables;
    mysql> EXIT;
