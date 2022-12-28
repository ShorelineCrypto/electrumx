FROM ubuntu:18.04

WORKDIR /

RUN apt-get update && \
        apt-get -y install python3-setuptools python3-multidict python3.7 python3.7-dev libleveldb-dev python3-setuptools python3-multidict gcc g++ libsnappy-dev zlib1g-dev libbz2-dev libgflags-dev build-essential python3-pip git

RUN python3.7 -m pip install --upgrade pip
RUN python3.7 -m pip install aiohttp pylru Cython uvloop quark_hash
RUN python3.7 -m pip install   plyvel==1.3.0
RUN git clone https://github.com/ShorelineCrypto/electrumx /opt/electrumx

ENV COIN=Dogecoin
ENV DB_DIRECTORY=/db
ENV DAEMON_URL="http://RPCUSER:RPCPASSWORD@IP:RPCPORT/"
ENV SERVICES="tcp://:10060,rpc://0.0.0.0:8001,ssl://:20060"
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

RUN python3.7 setup.py install
CMD ["/usr/bin/python3.7", "/usr/local/bin/electrumx_server"]

