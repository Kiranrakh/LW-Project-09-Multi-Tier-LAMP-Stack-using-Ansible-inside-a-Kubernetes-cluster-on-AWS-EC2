FROM ubuntu:20.04

ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=lampdb

RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y mysql-server && \
    apt clean && rm -rf /var/lib/apt/lists/*

COPY mysqld.cnf /etc/mysql/mysql.conf.d/mysqld.cnf

EXPOSE 3306

CMD ["mysqld"]
