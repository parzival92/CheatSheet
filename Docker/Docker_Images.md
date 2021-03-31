### Docker Images

How to create your own image(Webserver using flask)
1) OS
2) update apt repo
3) Install dependencies
4) Install python dependencies using pip
5) Copy source code to /opt folder
6) Run the web server using flask command


* **Docker file**

Instruction ====   arguments
From                ubuntu
RUN                 apt-get update
RUN                 apt-get install python
RUN                 pip install flask flask-mysql
COPY                . /opt/source-code
ENTRYPOINT          FLASK_APP=/opt/source-code/app.py flask run

* **How to build an image and push it to dockerhub**

```
docker build . -t username/imagename >> execute where your docker file is located
docker push >> also docker login
```

* **Environment Variables**
Inspect the environment variables set on the running container
```
docker inspect containerid
docker run -e envvarname=value --name nameofcontainer <imagename>
```
* **Command vs EntryPoint**
Command - We use command if we want to user to specify command at docker run 

CMD["node","--version"]

docker run image - print node version

docker run image npm --version - print npm version - override cmd

Entrypoint - Entrypoint means whatver entrypoint is used will get appended at docker run(you can override entrypoint)


For ex: ENTRYPOINT["node","--version]

you cannot pass docker run image npm version - error


