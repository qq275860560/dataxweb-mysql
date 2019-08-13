FROM qq275860560/base

MAINTAINER jiangyuanlin@163.com
# install mysql
RUN  yum -y install  http://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm &&\
    yum repolist enabled | grep mysql.*   &&\
    yum -y install mysql-community-server  &&\
    rm -rf /var/cache/yum/*

# init mysql   
RUN curl -fsSL "https://raw.githubusercontent.com/qq275860560/mysql/master/src/main/centos/tmp/init.sh" | sh 

RUN chmod -R 777 /var/lib/mysql /usr/share/mysql /var/run/mysqld &&\
    chown -R root:root /var/lib/mysql /usr/share/mysql /var/run/mysqld &&\
    cd /etc/ && curl -fsSL -O "https://raw.githubusercontent.com/qq275860560/dataxweb/master/src/main/centos/etc/my.cnf"  
   
    
RUN echo "import" &&\
    cd /usr/share/mysql/ && curl -fsSL -O "https://raw.githubusercontent.com/qq275860560/dataxweb/master/src/main/centos/usr/share/mysql/dataxweb.sql"

RUN  /usr/sbin/mysqld  --defaults-file=/etc/my.cnf --user=root --daemonize &&\
     mysql -uroot  -p123456  mysql< /usr/share/mysql/dataxweb.sql

  
CMD source /etc/profile &&\
    /usr/sbin/sshd &&\
     /usr/sbin/mysqld  --defaults-file=/etc/my.cnf --user=root --daemonize &&\
    tail -f /var/log/lastlog
   

 
