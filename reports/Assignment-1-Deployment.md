
## Deploy and Set Up Apache Cassandra Cluster

It is expected that Docker is installed on the system. 

In terminal cd into .../code and execute
`docker-compose up`

When the cluster sets up, get their container ids with 
`docker ps` and enter one of them with 
`docker exec -it <containerID> bash`

Enter CQL with `cqlsh` then create the needed keyspace for a tenant with
```
CREATE KEYSPACE data
  WITH REPLICATION = {
  'class' : 'SimpleStrategy',
  'replication_factor' : 3
  };
```
Then create table into the keyspace for our data with 
```
CREATE TABLE data.ddata (
time text,
readable_time timestamp,
acceleration float,
acceleration_x int,
acceleration_y int,
acceleration_z int,
battery int,
humidity float,
pressure float,
temperature float,
dev_id text,
PRIMARY KEY (dev_id, readable_time));
```

after that our nifi cluster is set ready for the data to be put into it.

## Deploy and Confugure Apache NiFi

In terminal pull latest Apache NiFi container: `docker pull apache/nifi:latest`


Deploy the container with


`docker run --name nifi -p 8443:8443 -e NIFI_WEB_HTTPS_PORT='8443' -d apache/nifi:latest`

The NiFi will generate a radom username and password. To see it, pen nifi container in terminal with `docker exec -it <container ID> /bin/sh/`

then `cd logs` and `cat nifi-app.log` ctrl+f / cmd+f Username to find the generated credentials.

<p align="center"><img src="img/credentials.png" width="500")<p>
