FROM debian:latest

RUN apt-get update && \
	apt-get install -y cowsay fortune

ENV PATH="/usr/games/:${PATH}"
COPY script.sh ~/

ENTRYPOINT ["~/script.sh"]
#CMD "cowsay | COWSAY"
