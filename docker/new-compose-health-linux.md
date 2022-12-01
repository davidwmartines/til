Instead of using scripts like wait-for-it.sh to ensure certain dependant containers are runinng in a compose stack,a more elegant solution is to leverage the healthcheck in docker compose. 

Notes:

 - On linux, to get the newer `docker compose` working (instead of having to use `docker-compose`) the **docker-compose-plugin** needs to be installed.
 - The `version` at the top of the compose file is not needed, and should be left out.
 
 
Example:

```
services:

  zookeeper:
    image: bitnami/zookeeper:3.7.0
    hostname: zookeeper
    container_name: zookeeper

    healthcheck:
      test: echo srvr | nc zookeeper 2181 || exit 1
      interval: 5s
      retries: 20

  kafka:
    image: bitnami/kafka:3.3.1
    hostname: kafka
    container_name: kafka
 
    healthcheck:
      test: kafka-topics.sh --list --bootstrap-server kafka:9092
      interval: 5s
      retries: 20

  schema-registry:
    image: confluentinc/cp-schema-registry:6.2.0
    hostname: schema-registry
    container_name: schema-registry
    depends_on:
      kafka:
        condition: service_healthy
  
    healthcheck:
      test: curl --write-out 'HTTP %{http_code}' --fail --silent --output /dev/null http://localhost:8081
      interval: 5s
      retries: 20

```
