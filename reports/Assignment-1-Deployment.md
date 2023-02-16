
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
