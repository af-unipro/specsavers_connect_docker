FROM mysql:latest

RUN sed -i -e 's/^max_allowed_packet.*/max_allowed_packet = 8000000000/' /etc/mysql/my.cnf

CMD ["mysqld"]

WORKDIR /var/lib/mysql
