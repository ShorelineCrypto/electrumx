FROM debian:stretch-slim

WORKDIR /

RUN apt-get update && \
        apt-get -y install ppython3-pip build-essential libc6-dev libncurses5-dev libncursesw5-dev

RUN apt -y install libreadline6-dev/stable libreadline6/stable
RUN apt-get -y install libleveldb-dev git

RUN pip3 install plyvel
RUN git clone https://github.com/ShorelineCrypto/electrumx /opt/electrumx

ENV COIN=Nengcoin
ENV DB_DIRECTORY=/db
ENV DAEMON_URL="http://RPCUSER:RPCPASSWORD@IP:RPCPORT/"
ENV SERVICES="tcp://:10001,rpc://0.0.0.0:8001,ssl://:10002"
ENV EVENT_LOOP_POLICY=uvloop
ENV PEER_DISCOVERY=self
ENV INITIAL_CONCURRENT=50
ENV COST_SOFT_LIMIT=10000
ENV COST_HARD_LIMIT=100000
ENV BANDWIDTH_UNIT_COST=10000
ENV SSL_CERTFILE=/ssl/server.crt
ENV SSL_KEYFILE=/ssl/server.key
ENV ALLOW_ROOT=true
ENV MAX_SEND=10000000
ENV CACHE_MB=2000

VOLUME /db
VOLUME /ssl

RUN mkdir -p "$DB_DIRECTORY" && ulimit -n 1048576
RUN mkdir -p /ssl

WORKDIR  /opt/electrumx

RUN python3 setup.py install
CMD ["/usr/bin/python3", "/usr/local/bin/electrumx_server"]

