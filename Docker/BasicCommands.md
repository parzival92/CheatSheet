### Docker Commands 

Docker run - Run container

```
Docker run centos
docker run -it centos bash
```


Remove Container

```
docker rm <containerid> or <name>
```
Docker Images

```
docker rmi centos
docker pull <image_name>
````

Run Command on  Running Container

```
docker exec <container_id> cat /etc/hosts/
docker exec mysql-db mysql -p db_pass123 -e 'use foo; select * from myTable'
```


