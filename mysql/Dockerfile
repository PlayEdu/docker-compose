FROM mysql:5.7.42

LABEL maintainer="Mahmoud Zalt <mahmoud@zalt.me>"

# 时区配置
ARG TZ=UTC
ENV TZ ${TIMEZONE}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ >/etc/timezone && chown -R mysql:root /var/lib/mysql/

# 复制自定义的my.cnf
COPY my.cnf /etc/mysql/conf.d/my.cnf

# 初始化数据库
COPY docker-entrypoint-initdb.d /docker-entrypoint-initdb.d

# my.cnf只读权限
RUN chmod 0444 /etc/mysql/conf.d/my.cnf

# 暴露3306端口
EXPOSE 3306

# 启动mysql
CMD ["mysqld"]
