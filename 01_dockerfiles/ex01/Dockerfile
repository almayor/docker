FROM debian

WORKDIR /home/teamspeak

ENV TS3SERVER_LICENSE=accept

RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y wget bzip2 && \
	rm -rf /var/lib/apt/lists

RUN wget http://dl.4players.de/ts/releases/3.12.1/teamspeak3-server_linux_amd64-3.12.1.tar.bz2 && \
	tar xvf teamspeak3-server_linux_amd64-3.12.1.tar.bz2 && \
	rm teamspeak3-server_linux_amd64-3.12.1.tar.bz2

# 9987 - default voice
# 10011 - server query
# 30033 - file transport

EXPOSE 9987/udp 10011 30033

ENTRYPOINT ["teamspeak3-server_linux_amd64/ts3server_minimal_runscript.sh"]

# https://www.vultr.com/docs/how-to-install-teamspeak-3-server-on-debian-9-stretch
# docker build -t ex01 .
# docker run -p 9987:9987/udp -p 10011:10011 -p 30033:30033 --name teamspeak ex01
# then use the ServerAdmin privilege key (token) to connect
# (no need to specify connection port)
