#### Chapter 4

In this chapter you will learn:

- Bridge and Host network in containers.

```shell
# If you are following from chapter 1, please remove the existing running in order to create the same name container.

# [Optional] I am using 🙈 kill but for graceful shut down please use stop
docker kill postgres
docker rm postgres

# 1. Bridge network demonstration

# Create a network
docker network create app-network

# Run postgres container in bridge network mode
docker run --rm \
  --name postgres \
  -e POSTGRES_USER=sally \
  -e POSTGRES_PASSWORD=softKitty \
  -e POSTGRES_DB=app \
  --network=app-network \
  postgres:16.0-alpine3.18

# Run PGAdmin in host network mode
docker run --rm -ti --name pgadmin \
  -p 8080:80 \
  --network app-network \
  dpage/pgadmin4

# Access PGAdmin on http://localhost:8080

# Once you done, Tear down the service
docker stop postgres pgadmin
docker rm postgres pgadmin

# 2. Host network demonstration
# Look here we are not exposing any port but still able to access postgres
docker run --rm \
  --name postgres \
  -e POSTGRES_USER=sally \
  -e POSTGRES_PASSWORD=softKitty \
  -e POSTGRES_DB=app \
  --network=host \
  postgres:16.0-alpine3.18

# Access postgres directly on port 5432 of host machine
```
