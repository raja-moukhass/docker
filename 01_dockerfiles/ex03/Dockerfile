FROM ubuntu:latest

EXPOSE 80 443 2222

RUN apt-get update  && apt-get upgrade -y &&\
		DEBIAN_FRONTEND=noninteractive apt-get install apt-utils apt-transport-https curl openssh-server ca-certificates postfix -y && \
		DEBIAN_FRONTEND=noninteractive curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
		DEBIAN_FRONTEND=noninteractive apt-get install -y gitlab-ce && \
		DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata

WORKDIR /etc/gitlab

# Generate Cerificate and keys
RUN mkdir -p /etc/gitlab/ssl && \
	chmod u=rwx /etc/gitlab/ssl/ && \
	openssl req -newkey rsa:4096 -nodes -x509 -subj "/C=MA/ST=Khouribga/L=Khouribga/O=1337/CN=10.11.11.1/emailAddress=ramoukha@student.1337.ma" \
	-keyout /etc/gitlab/ssl/selfsigned.key -out /etc/gitlab/ssl/selfsigned.crt

# configure gitlab for HTTPS
RUN sed -i 's/http:\/\/gitlab.example.com/https:\/\/10.11.11.1/' gitlab.rb
RUN echo "nginx['enable'] = true" >> gitlab.rb
RUN echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb
RUN echo "nginx['ssl_certificate'] = '/etc/gitlab/ssl/selfsigned.crt'" >> gitlab.rb
RUN echo "nginx['ssl_certificate_key'] = '/etc/gitlab/ssl/selfsigned.key'" >> gitlab.rb
RUN	echo "gitlab_rails['gitlab_shell_ssh_port'] = 2222" >> gitlab.rb
RUN echo "Port 2222" >> /etc/ssh/sshd_config

WORKDIR /

RUN echo "/opt/gitlab/embedded/bin/runsvdir-start& gitlab-ctl reconfigure" > start.sh && \
	echo "service ssh restart" >> start.sh && \
	echo "echo 'Done!'" >> start.sh && \
	echo "tail -f /dev/null" >> start.sh && \
	chmod 777 start.sh

CMD ["sh", "start.sh"]

#docker run -it --privileged -p 80:80 -p 443:443 -p 2222:2222 img
