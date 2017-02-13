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
