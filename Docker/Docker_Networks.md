### Networking in Docker

Three type of networks

1)Bridge - Default docker network usually assigned ip range 17.17 > for connectivity on host you need to expose ports.
2)None - Isolated 
3)Host - Running container on host network - Blocks ip 

User defined Network
------------------
```
docker network create --driver bridge --subnet 182.18.0.1/24 --gateway 182.18.0.1 wp-mysql-network
```

### Docker Registry

image: nginx >> user / image name 
default >> docker.io
docker.io/users/image

Private Registry (Cloud)
-----------------------
docker login private-registry.io

How to deploy your own registry (on prem)
------------------------------
docker run -d -p 5000:5000 --name registry registry:2