# YAML Docker Compose
The YAML in this repository will create one network and up two containers running in the same network and those containers are running in the same network, they look each other. In the WAS is need configure the libraries(WAS will can see the libraries because the path is shared) and JDBC connections.

Before use the YAML file to up the containers, follow these steps:
* Create in your Linux SO (VM) in the path `$HOME` one folder called: `citi-dependencies`, so, after that we have: `$HOME/citi-dependencies`;
* Inside `$HOME/citi-dependencies` create two others folders like `$HOME/citi-dependencies/was` and `$HOME/citi-dependencies/oracle`;

That folders will be shared with Oracle and WAS containers in the YAML file.

To run the YAML file is needed have all enviroment in Linux SO (or other SO) to Docker configured. To do that, follow the steps here: https://github.com/learn-docker-and-coding/start-with-docker
