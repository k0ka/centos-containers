FROM registry.access.redhat.com/ubi8/ubi 
LABEL maintainer="admin@idwrx.com"
LABEL description="Puppet server"

ENV YUM_CMD="dnf -y --disableplugin=subscription-manager"

RUN $YUM_CMD clean all
RUN $YUM_CMD update
RUN $YUM_CMD autoremove
RUN $YUM_CMD install https://yum.puppetlabs.com/puppet-release-el-8.noarch.rpm
RUN $YUM_CMD --nodocs install puppetserver-6.8.0-1.el8
RUN $YUM_CMD clean all

EXPOSE 8140/tcp

VOLUME ["/etc/puppetlabs", "/opt/puppetlabs/server/data/puppetserver", "/var/log/puppetlabs/puppetserver"]

CMD ["/opt/puppetlabs/bin/puppetserver", "foreground"]
