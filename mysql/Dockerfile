FROM mysql:5.7.42

LABEL maintainer="Mahmoud Zalt <mahmoud@zalt.me>"

ARG TZ=UTC
ENV TZ ${TIMEZONE}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ >/etc/timezone && chown -R mysql:root /var/lib/mysql/

COPY my.cnf /etc/mysql/conf.d/my.cnf
COPY docker-entrypoint-initdb.d /docker-entrypoint-initdb.d

RUN chmod 0444 /etc/mysql/conf.d/my.cnf

CMD ["mysqld"]

EXPOSE 3306
