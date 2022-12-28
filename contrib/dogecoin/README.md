## Install electrumx docker image for Dogecoin on x86_64 (amd64) or arm64 (aarch64) GNU/linux: 
Build docker image with:

```
  docker build -t electrumx-doge .
```

## Run electrumx Dogecoin server with docker

Replace with your DOGE full node rpcuser/rpcpassword and your server hostname with below command, assuming the DOGE full node runs at rpcport=22555 :

```
  docker run -d --net=host -v /opt/electrumx/db-DOGE/:/db -v /opt/electrumx/ssl:/ssl -e DAEMON_URL="http://youruser:yourpass@127.0.0.1:22555" -e REPORT_SERVICES=tcp://yourhost:10060,ssl://yourhost:20060 electrumx-doge
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

## Shut down electrum Dogecoin docker server
 for a proper clean shutdown, send TERM signal to the running container eg.: 

```
  docker kill --signal="TERM" CONTAINER_ID

```

## clean up and remove residual containers

Stopped containers take up disk and memory resources, you may want to clean up and remove those dead containers to free up resources

```
  docker rm CONTAINER_ID
```

## electrumx server crash maintenance

Electrumx server tend to crash from time to time after running smoothly for several weeks.  Using docker logs CONTAINER_ID method can find 
crash error like this assuming your CONTAINER_ID is 'c39a7d4a07d7': 
```
  docker ps -a
  docker logs c39a7d4a07d7

--- skipped logs informations ---
  struct.error: 'H' format requires 0 <= number <= 65535
```

The ROOT CAUSE of the crash is due to database overflow and can be fixed with below steps  :

#### (1) delete the exited docker container
```
   docker ps -a
   docker rm c39a7d4a07d7
```

#### (2) setup "test" container to do maintenance job
```
    docker run -it --name test  -v /opt/electrumx/db-DOGE/:/db   electrumx-doge  /bin/bash
```

This above command will enter docker container with root account.
#### (3) do maintenance in "test" container

Run below commands inside container root account in electrumx folder  /opt/electrumx

```
   python3.7 electrumx_compact_history
   exit
```

The above python3.7 command should take a few minutes to complete and then exit container


#### (4) Delete the containers and re-start electrumx-doge container job
```
   docker rm test
```
   go back to command step above under "Run electrumx Dogecoin server with docker"

