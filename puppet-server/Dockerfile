FROM centos:8 

ENV PUPPET_VERSION="6.8.0-1" \
	SUMMARY="Platform for running puppet server $PUPPET_VERSION" \
	DESCRIPTION="Puppet provides tools to automate managing your infrastructure. "

LABEL \ 
	maintainer="admin@idwrx.com" \
    summary="${SUMMARY}" \
    description="${DESCRIPTION}" \
    name="idwrx/puppet-server"

RUN	dnf -y clean all &&\
	dnf -y update && \
	dnf -y autoremove && \
	dnf -y clean all && \
	dnf -y install https://yum.puppetlabs.com/puppet-release-el-8.noarch.rpm && \
	dnf -y install puppetserver-${PUPPET_VERSION}.el8

EXPOSE 8140/tcp


VOLUME ["/etc/puppetlabs", "/opt/puppetlabs/server/data/puppetserver", "/var/log/puppetlabs/puppetserver"]

CMD ["/opt/puppetlabs/bin/puppetserver", "foreground"]
