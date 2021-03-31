### DOCKER RUN COMMANDS

Run - Tag

```
docker run ubuntu:18.04
```
* **Docker run with detach mode - To run container in background and give you console.**

```
docker run -d ubuntu sleep 1000
```

* **Let's Play with jenkins image**

```
docker pull jenkins:2.60.3
docker run jenkins
```

As no port mapping is enabled it will be available via internal ip or you need to enabled port mapping to access from docker host.

```
docker run -p 8080:8080 jenkins
```





