# How to Set up Electrumx Server with Docker Method

The fast simple method requires Ubuntu 18.04 server. This is as your linux server might run newer ubuntu or debian versions. When you need to run two coins (nengcoin and cheetahcoin)
electrumx services in same server machine, the fast simple method is difficult to manage.

Here is the a method that you can easily run docker jobs of 2 coins (nengcoin and cheetahcoin) in any gnu linux machines.


## Run NENG or CHTA Full Node

In the same electrum server, you will need to run nengcoin and/or cheetahcoin full node.  Download latest version of core wallet, set up proper
rpc username/password and rpc port in the "nengcoin.conf" and/or "cheetahcoin.conf" in their proper wallet folder, run full node and
sync the full node to latest block.

Copy down the rpcuser/rpcpassword/rpcport information, they will be used in below electrumx server configuration.

## Prepare electrumx folders

Ran below:
```
sudo mkdir -p /opt/electrumx/db-NENG
sudo mkdir -p /opt/electrumx/db-CHTA
```
The above commands created proper folders that will be used in docker run jobs

## Create SSL certificat

Ran below to create SSL certificat needed for electrum ssl connection. 
```
  cd /opt/electrumx/
  mkdir -p ssl

  cd ssl

  openssl genrsa -out server.key 2048
  openssl req -new -key server.key -out server.csr
  openssl x509 -req -days 1825 -in server.csr -signkey server.key -out server.crt
```



## Install docker

In ubuntu or debian, you can run below to install docker in your linux machine:

```
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
 sudo apt-get update
 sudo apt-get install -y docker-ce
```

Check out online guide if your linux is openSUSE, fedora or arch based.


## Install coin docker images, run docker job

For Nengcoin,  checkout 'contrib/nengcoin' of this repos README guide, follow the guide step by step to install docker image, run a docker-run job, and trouble shoot
job log information or other maintanence tasks if needed.

For Cheetahcoin, checkout 'contrib/cheetahcoin' (pending).

Your can run 2 coins with docker jobs together in the same linux server. 

The electrumx server should be running now allow electrum-NENG or electrum-CHTA to connect to your server.
