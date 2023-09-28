#### Chapter 1

In this chapter you will learn:

- How to pull an OCI image
- How to run a container from the image

```shell
# Make sure in your system docker is installed and running
docker pull postgres:16.0-alpine3.18

# Run the postgres image
docker run --rm \
  --name postgres \
  -e POSTGRES_USER=sally \
  -e POSTGRES_PASSWORD=softKitty \
  -e POSTGRES_DB=app \
  postgres:16.0-alpine3.18

# See the image is running
docker ps

# Wait but how can I see access the postgres from my host machine?
# There are two ways
# 1. Using docker inspect to get the IP address of the container
docker inspect --format '{{ .NetworkSettings.Networks.bridge.IPAddress }}' postgres
# 1.1 Use this IP to connect to postgres from your host machine
psql --host=<container IP address> --username=sally

# 2. Expose the postgres port and link it to your host
docker run --rm -d --name postgres -p 5432:5432 postgres:16.0-alpine3.18

# Now you can connect using localhost:5432 instead of container IP
```
