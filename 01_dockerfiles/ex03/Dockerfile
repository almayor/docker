FROM debian

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y ca-certificates openssh-server curl postfix tzdata

RUN curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && apt-get install -y gitlab-ce

COPY gitlab.rb /etc/gitlab/
COPY server.cert /etc/gitlab/ssl/
COPY server.key /etc/gitlab/ssl/

EXPOSE 443 80 22
ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && /etc/init.d/ssh start && tail -f /dev/null

# docker build -t ex03 . && docker run -it --rm -p 8080:80 -p 8022:22 -p 8443:443 --privileged ex03
# Then register on https://localhost:8443 (default username is root)
# git clone https://localhost:8443/<user>/<repo>
# git clone ssh://git@localhost:8022/<user>/<repo> (add your ssh key to Gitlab beforehand)