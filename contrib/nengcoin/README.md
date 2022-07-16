## Install electrumx docker image for Nengcoin 
Build docker image with:

```
  docker build -t electrumx-neng .
```

## Run electrumx Nengcoin server with docker

Replace with your NENG full node rpc user/rpc password with below commands, assuming the NENG full node runs at rpcport=8388 :

```
  docker run -d --net=host -v /opt/electrumx/db-NENG/:/db -v /opt/electrumx/ssl:/ssl -e DAEMON_URL="http://youruser:yourpass@127.0.0.1:8388" -e REPORT_SERVICES=ssl://electrum.shorelinecrypto.com:10002 electrumx

```

## Shut down electrum Nengcoin docker server
 for a proper clean shutdown, send TERM signal to the running container eg.: 

```
  docker kill --signal="TERM" CONTAINER_ID

```

