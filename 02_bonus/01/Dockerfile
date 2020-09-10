FROM gcc:latest

# Solving "Hash mismatch" errors
# RUN export DEBIAN_FRONTEND=noninteractive
# RUN rm -rf /var/lib/apt/lists/
# RUN echo 'Acquire::CompressionTypes::Order:: "gz";' >> /etc/apt/apt.conf
# RUN apt-get clean

RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install --no-install-recommends -y \
		apt-utils \
		valgrind \
		nano && \
	rm -rf /var/lib/apt/lists

CMD ["bash"]
