# YAML Docker Compose
The YAML in this repository will create one network and up two containers running in the same network and those containers are running in the same network, they look each other. In the WAS is need configure the libraries(WAS will can see the libraries because the path is shared) and JDBC connections.

Before use the YAML file to up the containers, follow these steps:
* Create in your Linux SO (VM) in the path `/opt/` one folder called: `citi-dependencies`, so, after that we have: `/opt/citi-dependencies`;
* Inside `/opt/citi-dependencies` create two others folders like `/opt/citi-dependencies/was` and `/opt/citi-dependencies/oracle`;
* To do that just execute: `mkdir -p /opt/{citi-dependencies/{was,oracle}}`;

That folders will be shared with Oracle and WAS containers in the YAML file.

To run the YAML file is needed have all enviroment in Linux SO (or other SO) to Docker configured. To do that, follow the steps here: https://github.com/learn-docker-and-coding/start-with-docker

#### Start the WAS
* Execute on the WAS container:
```sh
docker exec -ti was sh -c "/opt/IBM/WebSphere/AppServer/profiles/Dmgr01/bin/startManager.sh && /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/bin/startNode.sh
```
* To access:
```js
http://localhost:28000/ibm/console
username: wasadmin
password: wasadmin
```
* Realize the configurations.

#### Oracle database
