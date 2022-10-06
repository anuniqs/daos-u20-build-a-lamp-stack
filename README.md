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



# U20, LAMP —( P ) PHP

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




# U20, LAMP —Apache2 Virtual Host

#### Create the directory for your_domain,

`anup@lamp:~$ sudo mkdir /var/www/html/anuniqstv.lamp.ek`

`anup@lamp:~$ sudo chown -R $USER:$USER /var/www/html/anuniqstv.lamp.ek`

#### Changes on main configuration,

`anup@lamp:~$ sudo nano /etc/apache2/apache2.conf`

    IncludeOptional conf-enabled/*.conf
    IncludeOptional sites-enabled/*.conf

And add a line containing ServerName 127.0.0.1 to the end of the file,

`ServerName 127.0.0.1`

#### Create a new configuration file in Apache’s sites-available,

`anup@lamp:~$ ls -ltr /etc/apache2/sites-available`

`anup@lamp:~$ ls -ltr /etc/apache2/sites-enabled/`

`anup@lamp:~$ sudo cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf.backup`

`anup@lamp:~$ sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf.backup`

`anup@lamp:~$ sudo nano /etc/apache2/sites-available/anuniqstv.lamp.ek.conf`

    <VirtualHost *:80>
    ServerName 192.168.56.12
    ServerAlias 192.168.56.12  
    ServerAdmin uniqs.anup@gmail.com
    DocumentRoot /var/www/html/anuniqstv.lamp.ek 

    <Directory /var/www/html/anuniqstv.lamp.ek>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/anuniqstv.lamp.ek-error.log
    CustomLog ${APACHE_LOG_DIR}/anuniqstv.lamp.ek-access.log combined
</VirtualHost>
#### Enable new configuration,

`anup@lamp:~$ sudo a2ensite anuniqstv.lamp.ek`

`anup@lamp:~$ sudo systemctl reload apache2.service`

`anup@lamp:~$ ls -ltr /etc/apache2/sites-available`

`anup@lamp:~$ ls -ltr /etc/apache2/sites-enabled/`

#### Disable default configuration,

`anup@lamp:~$ sudo a2dissite 000-default`

`anup@lamp:~$ sudo systemctl reload apache2.service`

`anup@lamp:~$ ls -ltr /etc/apache2/sites-enabled/`

#### Test configuration,

`anup@lamp:~$ sudo apache2ctl configtest`

`anup@lamp:~$ sudo journalctl -u apache2.service --since today --no-pager`

#### Create an index.html file,

`anup@lamp:~$ nano /var/www/html/anuniqstv.lamp.ek/index.html`

    <html>
        <head>
            <title> LAMP Server</title>
        </head>
        <body>
            <h1>Hey ! from <em> anuniqsTV</em>. </h1>
    <p>Works fine !</p>
        </body>
    </html>
`anup@lamp:~$ sudo systemctl reload apache2.service`

### Access,

`anup@lamp:~$ telnet 192.168.56.12 80`

`anup@lamp:~$ curl -Is http://192.168.56.12 | head -1`

### Open your favorite browser : [http://192.168.56.12/](http://192.168.56.12/ "http://192.168.56.12/")
