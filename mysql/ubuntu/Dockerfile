
FROM ubuntu:latest
MAINTAINER lh


RUN apt-get update
# timezone
RUN apt-get install tzdata

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo 'Asia/Shanghai' >/etc/timezone
# Install MySQL
RUN \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends mysql-server mysql-client  && \
    apt-get autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    /etc/init.d/mysql stop && \
    rm -rf /var/lib/mysql/*
RUn mkdir -p /var/lib/mysql /var/run/mysqld
RUN chown 777 /var/lib/mysql 
RUN chmod 777 /var/run/mysqld

RUN sed -Ei 's/^(bind-address|log)/#&/' /etc/mysql/my.cnf \
    && echo 'skip-host-cache\nskip-name-resolve' | awk '{ print } $1 == "[mysqld]" && c == 0 { c = 1; system("cat") }' /etc/mysql/my.cnf > /tmp/my.cnf \
    && mv /tmp/my.cnf /etc/mysql/my.cnf
#
# The init-db scripts or sql command files in this directory will be executed when container created.
# The details please refer "entrypoint.sh"
#
RUN mkdir /docker-entrypoint-initdb.d

VOLUME /var/log/mysql
VOLUME /var/lib/mysql

EXPOSE 3306


COPY docker-entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["mysqld"]
