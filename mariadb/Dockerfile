FROM centos:8 

ENV	SUMMARY="Platform for running mariadb" \
	DESCRIPTION="MariaDB is a community-developed fork of MySQL intended to remain free under the GNU GPL."


LABEL maintainer="admin@idwrx.com" \
	summary="${SUMMARY}" \
	description="${DESCRIPTION}" \
	name="idwrx/mariadb"

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r -g 27 mysql && useradd -r -g mysql -u 27 mysql


RUN	dnf -y clean all && \
	dnf -y --nodoc --setopt=install_weak_deps=false update && \
    dnf -y erase acl bind-export-libs cpio dhcp-client dhcp-common dhcp-libs \
        ethtool findutils ipcalc iproute iputils kexec-tools \
        less lzo pkgconf pkgconf-m4 procps-ng shadow-utils snappy squashfs-tools \
        vim-minimal xz && \
	dnf -y autoremove && \
	dnf -y install --setopt=tsflags=nodocs mariadb-server && \
	dnf -y clean all 
	

COPY docker-entrypoint.sh /
RUN chmod 0755 /docker-entrypoint.sh
RUN chown 27:27 /var/lib/mysql

ENTRYPOINT ["/docker-entrypoint.sh"]
EXPOSE 3306/tcp

USER 27

CMD ["mysqld_safe"]
