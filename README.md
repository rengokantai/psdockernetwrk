# psdockernetwrk
##2. The Basics
###4 Hands on with the Basic Docker Networking Commands
```
docker network ls
```
```
docker network inspect bridge
```

##3. Use Cases and Drivers
###2 Single-host Networking
singlehost->bridge network  

######create
```
docker network create -d bridge --subnet 10.0.0.1/24 ps-bridge
```
```
apt install bridge-utils
```
```
brctl show
ip link show
```

create two containers (share bridge network)
```
docker run -dt --name c1 --network ps-bridge alpine sleep 1d
docker run -dt --name c2 --network ps-bridge alpine sleep 1d
```
inspect
```
docker network inspect ps-bridge
```


exercise
```
docker exec -it c1 sh
```
in the container
```
ip a
ping 10.0.0.3
ping c2
```
###3 Multi-host Overlay Networking
node1
```
docker swarm init --advertise-addr 10.17.0.5
ufw allow 2377
```

node1
```
docker node ls
docker network ls
```
create an overlay network
```
docker network create -d overlay ps-over
```
```
docker service create --name ps-svc --network ps-over --replicas 2 alpine sleep 1d
docker service ps ps-svc
```
