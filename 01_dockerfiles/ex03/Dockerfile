FROM debian

# Solving "Hash mismatch" errors
RUN export DEBIAN_FRONTEND=noninteractive
RUN rm -rf /var/lib/apt/lists/
RUN echo 'Acquire::CompressionTypes::Order:: "gz";' >> /etc/apt/apt.conf
RUN echo 'Acquire::http::Pipeline-Depth 0;' >> /etc/apt/apt.conf
RUN echo 'Acquire::http::No-Cache true;' >> /etc/apt/apt.conf
RUN echo 'Acquire::BrokenProxy true;' >> /etc/apt/apt.conf
RUN apt-get clean

RUN apt-get update \
	&& apt-get install --no-install-recommends -y \
		curl \
		openssh-server \
		ca-certificates \
		postfix \
		gnupg \
	&& rm -rf /var/lib/apt/lists/*

# Automate postfix installation
# https://serverfault.com/questions/143968/automate-the-installation-of-postfix-on-ubuntu
# RUN debconf-set-selections <<< "postfix postfix/mailname string 42-docker.local" \
# 	&& debconf-set-selections <<< "postfix postfix/main_mailer_type string 'Internet Site'" \
# 	&& apt-get update \
# 	&& apt-get install -y postfix \
# 	&& rm -rf /var/lib/apt/lists/*

ENV TERM=xterm
VOLUME ["/etc/gitlab", "/var/opt/gitlab", "/var/log/gitlab"]
EXPOSE 443 80 22

# Installation
# https://about.gitlab.com/install/#debian
RUN curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
	apt-get install -y gitlab-ce

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && tail -f /dev/null
