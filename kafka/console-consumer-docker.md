# Console-Consumer For Kafka in Docker Compose

This one-liner starts a console-consumer on a topic that is within a Kafka instance you have running within docker compose.  It runs the [kcat](https://github.com/edenhill/kcat) docker image and connects to the network of a running docker-compose project.

```sh
docker run -it --network <NETWORK_NAME> edenhill/kcat:1.7.0 -b <KAFKA_SERVICE_NAME>:<KAFKA_SERVICE_PORT> -C -t <TOPIC_NAME> -f 'Topic %t [%p] at offset %o: key %k: %s\n'

```

For example, if the project directory containing the docker-compose.yaml file is called `my-app`, and the docker-compose file defines a Kafka broker service instance called `kafka` on the default port of 9092, and you want to consume messages from a topic called `test_topic`, the command to run would be:

```sh
docker run -it --network my-app_default edenhill/kcat:1.7.0 -b kafka:9092 -C -t test_topic -f 'Topic %t [%p] at offset %o: key %k: %s\n'
```