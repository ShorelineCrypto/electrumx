## Install electrumx docker image for Nengcoin 
Build docker image with:

```
  docker build -t electrumx-neng .
```

## Run electrumx Nengcoin server with docker

Replace with your NENG full node rpcuser/rpcpassword and your server hostname with below command, assuming the NENG full node runs at rpcport=8388 :

```
  docker run -d --net=host -v /opt/electrumx/db-NENG/:/db -v /opt/electrumx/ssl:/ssl -e DAEMON_URL="http://youruser:yourpass@127.0.0.1:8388" -e REPORT_SERVICES=ssl://yourhost:10002 electrumx-neng
```

## Trouble shoot or check docker container status

Your docker run electrumx server job should be running, run below to obtain image / container ID

```
  docker ps
  docker container ls -la
  docker images -a
```

In order to trouble shoot issues or check log information of electrumx job, run blow to get real time log information 

```
  docker logs CONTAINER_ID
```

## Shut down electrum Nengcoin docker server
 for a proper clean shutdown, send TERM signal to the running container eg.: 

```
  docker kill --signal="TERM" CONTAINER_ID

```

## clean up and remove residual containers

Stopped containers take up disk and memory resources, you may want to clean up and remove those dead containers to free up resources

```
  docker rm CONTAINER_ID
```
