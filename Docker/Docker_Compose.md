## Docker Compose 
Version1
------------
* **No way specify network**
* **dependency Limitation in order of execution**

Version2
---------------
* **Services concept**
* **Links are not required(Automatically create bridge network and attahces all container within network)**
* **Note:You can specify version so that docker will know which version is getting used.**
version: 2
* **Depends on feature**

depends_on:
    redis

Version3
-----------------
version: 3
* **Supports for docker swarm**

Docker Compose Labs
-------------------------
First create a postgress database container called db, image postgres, environmental variable POSTGRES_PASSWORD=mysecretpassword
```
docker run -d -e POSTGRES_PASSWORD=mysecretpassword --name=db postgres

```
Next let's create a simple wordpress container called wordpress, image: wordpress, link it to the container db and expose it on host port 8085
```
docker run -d --name=wordpress --link db:db -p 8085:80 wordpress
```
Lets do above it docker-compose
Create a docker-compose.yml file under the path /root/wordpress. Once done, run a docker-compose up.
The compose file should have exact specification of the wordpress and db container
```
services:
  db:
    environment:
      POSTGRES_PASSWORD: mysecretpassword
    image: postgres
  wordpress:
    image: wordpress
    links:
    - db
    ports:
    - 8085:80
version: '3.0'

```
How will you convert version 1 to version 3

* **Add services and version 3**
* **No links required**



