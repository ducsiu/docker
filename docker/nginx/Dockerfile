FROM centos:centos7

# install nginx 1.16
RUN yum install  -y http://nginx.org/packages/centos/7/x86_64/RPMS/nginx-1.16.1-1.el7.ngx.x86_64.rpm

# install php 7.3
RUN yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y &&\
    yum install yum-utils -y &&\
    yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y &&\
    yum-config-manager --enable remi-php73 &&\
    yum install php73 -y &&\
    yum -y install php php-cli php-fpm php-mysqlnd php-zip php-devel php-gd php-mcrypt php-mbstring php-curl php-xml php-pear php-bcmath php-json php-mysql

# install Xdebug
WORKDIR /opt
RUN yum install git -y &&\
    yum install php-devel -y &&\
    git clone git://github.com/xdebug/xdebug.git
WORKDIR /opt/xdebug
RUN phpize && ./configure --enable-xdebug && make && make install &&\
    echo "zend_extension="/wherever/you/put/it/xdebug.so"" >> /etc/php.ini

EXPOSE 80

ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
