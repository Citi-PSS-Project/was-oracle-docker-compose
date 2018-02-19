# YAML Docker Compose
The YAML in this repository will create one network and up two containers running in the same network and those containers are running in the same network, they look each other. In the WAS is need configure the libraries(WAS will can see the libraries because the path is shared) and JDBC connections.

Before use the YAML file to up the containers, follow these steps:
* Create in your Linux SO (VM) in the path `/opt/` one folder called: `citi-dependencies`, so, after that we have: `/opt/citi-dependencies`;
* Inside `/opt/citi-dependencies` create two others folders like `/opt/citi-dependencies/was` and `/opt/citi-dependencies/oracle`;
* To do that just execute: 
```sh
sudo mkdir -p /opt/citi-dependencies/was && \
sudo mkdir -p /opt/citi-dependencies/oracle && \
sudo mkdir -p /opt/citi-dependencies/oracle/db && \
sudo mkdir -p /opt/citi-dependencies/oracle/scripts

sudo chmod 755 -R /opt/citi-dependencies
```

That folders will be shared with Oracle and WAS containers in the YAML file.

#### Execute the YAML file
First, clone the repository: `git clone https://github.com/Citi-PSS-Project/was-oracle-docker-compose.git` after, inside it, execute: 
* To up the containers: `sudo docker-compose --file citi-docker-compose.yaml up -d`
* To see the containers status: `sudo docker-compose --file citi-docker-compose.yaml ps`
* To stop and remove containers up: `sudo docker-compose --file citi-docker-compose.yaml down`

To run the YAML file is needed have all enviroment in Linux SO (or other SO) to Docker configured. To do that, follow the steps here: https://github.com/learn-docker-and-coding/start-with-docker

#### Start the WAS
* Access the container:
```sh
sudo docker exec -it was bash
```
* Execute WAS on the container:
```sh
sh /opt/IBM/WebSphere/AppServer/profiles/Dmgr01/bin/startManager.sh && \
sh /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/bin/syncNode.sh && \ 
sh /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/bin/startNode.sh
```
* After the container started, just execute `exit` to go out the bash console;
* To access the admin console:
```js
http://localhost:28000/ibm/console
username: wasadmin
password: wasadmin
```
* Realize the configurations: 
1. Copy all libraries needed to path: `/opt/citi-dependencies/was`;
2. In web admin WAS interface, when need point some library, the path to show is `/home` (the libraries copy to the path in the instruction 1 will be here in this path);

#### Oracle database
Access host database:
```js
hostname: localhost
port: 1521
sid: xe
username: system
password: oracle
Password for SYS user
```

Access admin web interface:
```js
url: http://localhost:8080/apex
workspace: internal
user: admin
password: oracle
```

#### Oficial documentation
https://docs.docker.com/engine/reference/commandline/exec/#examples

#### Links
https://hub.docker.com/r/ibmcom/websphere-traditional/
http://veithen.github.io/2014/11/02/running-was-in-docker.html
https://docs.docker.com/samples/library/websphere-liberty/
