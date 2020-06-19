# https://www.vultr.com/docs/how-to-install-teamspeak-3-server-on-debian-9-stretch
# docker run --rm -p 127.0.0.1:9987:9987/udp -p 127.0.0.1:10011:10011 -p 127.0.0.1:30033:30033 --name teamspeak -d ex01

FROM debian

ENV TS3SERVER_LICENSE=accept
EXPOSE 9987/udp 10011 30033
WORKDIR /home/teamspeak

RUN apt-get update && \
	apt-get install -y wget bzip2 && \
	rm -rf /var/lib/apt/lists

RUN wget http://dl.4players.de/ts/releases/3.12.1/teamspeak3-server_linux_amd64-3.12.1.tar.bz2 && \
	tar xvf teamspeak3-server_linux_amd64-3.12.1.tar.bz2 && \
	rm teamspeak3-server_linux_amd64-3.12.1.tar.bz2

CMD ["sh", "teamspeak3-server_linux_amd64/ts3server_minimal_runscript.sh", "start"]
