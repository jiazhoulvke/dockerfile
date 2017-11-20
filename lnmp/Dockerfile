FROM ubuntu:16.04

MAINTAINER jiazhoulvke@gmail.com

RUN sed -i "s/archive.ubuntu.com/cn.archive.ubuntu.com/g" /etc/apt/sources.list && \
        apt-get update && \
        apt-get upgrade -y && \
        apt-get install -y openssh-server vim htop wget unzip curl bash-completion nginx mysql-client libmysqlclient-dev php7.0 php7.0-bcmath php7.0-cli php7.0-curl php7.0-dev php7.0-fpm php7.0-gd php7.0-json php7.0-mcrypt php7.0-mysql php7.0-sqlite3 php7.0-xml php7.0-zip supervisor && \
        DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server && \
        apt-get clean && \
        sed -i "s/prohibit-password/YES/" /etc/ssh/sshd_config && \
        sed -i "s/127.0.0.1/0.0.0.0/" /etc/mysql/mysql.conf.d/mysqld.cnf && \
        sed -i "s/run\/php\/php7.0/run\/php7.0/" /etc/php/7.0/fpm/php-fpm.conf && \
        sed -i "s/run\/php\/php7.0/run\/php7.0/" /etc/php/7.0/fpm/pool.d/www.conf && \
        rm -fr /var/lib/mysql/* && \
        rm -rf /var/lib/apt/lists/* && \
        echo "source /etc/bash_completion" >> /root/.bashrc && \
        echo "alias ..='cd ..'" >> /root/.bashrc && \
        echo "alias ...='cd ../..'" >> /root/.bashrc && \
        echo "alias ....='cd ../../..'" >> /root/.bashrc && \
        echo "daemon off;" >> /etc/nginx/nginx.conf && \
        rm -fr /var/www/html && \
        mkdir -p /var/run/sshd && \
        mkdir -p /var/run/mysqld && \
        chmod a+rw /var/run/mysqld && \
        mkdir -p /var/log/supervisor && \
        mkdir -p /root/.ssh && \ 
        echo 'root:root' | chpasswd

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY nginx_default /etc/nginx/sites-available/default
COPY _vimrc /root/.vimrc
COPY entrypoint.sh /entrypoint.sh
COPY composer.phar /usr/local/bin/composer

EXPOSE 22 80 3306

VOLUME ["/var/www"]

CMD ["/entrypoint.sh"]
