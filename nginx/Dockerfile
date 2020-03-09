FROM centos:8 

ENV NGINX_VERSION=1.16 \
	SUMMARY="Platform for running nginx $NGINX_VERSION" \
	DESCRIPTION="Nginx is a web server and a reverse proxy server for HTTP, SMTP, POP3 and IMAP \
protocols, with a strong focus on high concurrency, performance and low memory usage. The container \
image provides a containerized packaging of the nginx $NGINX_VERSION daemon. The image can be used \
as a base image for other applications based on nginx $NGINX_VERSION web server."


LABEL maintainer="admin@idwrx.com" \
	summary="${SUMMARY}" \
	description="${DESCRIPTION}" \
	name="idwrx/nginx"

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r nginx && useradd -r -g nginx nginx


RUN	dnf -y clean all && \
	dnf -y update && \
	dnf -y autoremove && \
	dnf -y module enable nginx:$NGINX_VERSION && \
	dnf -y install --setopt=tsflags=nodocs nginx && \
	dnf -y clean all 
	

EXPOSE 80/tcp


VOLUME ["/etc/nginx", "/var/log/nginx"]

CMD ["/usr/sbin/nginx", "-g", "daemonf off;"]
