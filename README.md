
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
