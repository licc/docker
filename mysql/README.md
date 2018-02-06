debian
support arm64
docker run --name aarch64mysql5.5 -p 3306:3306 -v /data/mysql/debian/mysql_data:/var/lib/mysql -v /data/mysql/debian/conf/my.cnf:/etc/mysql/my.cnf -v /data/mysql/debian/logs:/var/log/mysql -e MYSQL_ROOT_PASSWORD=123456 -d debian/mysql5.5:latest


ubuntu
docker run --name ubuntumysql5.7 -p 3306:3306   -v /data/mysql/ubuntu/conf/:/etc/mysql/mysql.conf.d/  -v /data/mysql/ubuntu/mysql_data:/var/lib/mysql -v /data/mysql/ubuntu/logs:/var/log/mysql -e MYSQL_ROOT_PASSWORD=123456  -d ubuntu/mysql5.7.21:latest
