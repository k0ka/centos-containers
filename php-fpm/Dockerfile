FROM centos:8 

ENV USER_ID=900 \
	GROUP_ID=900 \
	PHP_VERSION="7.4" \
	SUMMARY="Platform for running Remi's php-fpm ${PHP_VERSION} on CentOS 8" \
	DESCRIPTION="PHP-FPM (FastCGI Process Manager) is an alternative PHP FastCGI \
		implementation with some additional features useful for sites of any size, \
		especially busier sites."


LABEL maintainer="admin@idwrx.com" \
	summary="${SUMMARY}" \
	description="${DESCRIPTION}" \
	name="idwrx/php-fpm"

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r -g $GROUP_ID php-fpm && useradd -r -g php-fpm -u $USER_ID php-fpm


RUN	dnf -y clean all && \
    dnf -y --nodoc --setopt=install_weak_deps=false update && \
    dnf -y erase acl bind-export-libs cpio dhcp-client dhcp-common dhcp-libs \
        ethtool findutils hostname ipcalc iproute iputils kexec-tools \
        less lzo pkgconf pkgconf-m4 procps-ng shadow-utils snappy squashfs-tools \
        vim-minimal xz && \
	dnf -y autoremove && \
	dnf -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm && \
	dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm && \ 
	dnf -y update && \
	dnf -y module reset php && \
	dnf -y module enable php:remi-${PHP_VERSION} && \
	dnf -y install --setopt=tsflags=nodocs php php-fpm php-phpiredis php-pecl-memcache php-pecl-memcached php-mysqlnd && \
	dnf -y clean all 

COPY ./php-fpm.conf /etc/php-fpm.conf
COPY ./global.conf /etc/php-fpm.d/global.conf
COPY ./www.conf /etc/php-fpm.d/www.conf
	
EXPOSE 9000/tcp

USER php-fpm 

CMD ["/usr/sbin/php-fpm", "-F"]
