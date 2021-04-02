### Docker Storage

volumes

* **if you want to use default location for volumes**
```
docker run -v data_volume:/var/lib/mysql mysql
```
Note: if particular folder doesn't exist it will create

* **If you want to use difference location for volumes**
```
docker run -v d:/dockerubuntu:var/lib/mysql -e MYSQL_ROOT_PASSWORD=couldbeanything mysql
```
Two type of mounts

1- Volume mounts - volume folder from default location(/var/lib/docker/volumes/dockubuntu)
2) Bind mounts - Directory from any location on docker host

Use mount keywword 
```
docker run \
--mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql
```
##### Note:
If you use -v or --volume to bind-mount a file or directory that does not yet exist on the Docker host, -v creates the endpoint for you. It is always created as a directory.

If you use --mount to bind-mount a file or directory that does not yet exist on the Docker host, Docker does not automatically create it for you, but generates an error.