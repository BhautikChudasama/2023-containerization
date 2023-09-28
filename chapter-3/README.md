#### Chapter 3

In this chapter you will learn:

- Volume mounts and data persistence in containers.

```shell
# If you are follwing from chapter 1, please remove the existing running in order to create the same name container.

# [Optional] I am using 🙈 kill but for graceful shut down please use stop
docker kill postgres
docker rm postgres

# Again running the postgres container
docker run --rm \
  --name postgres \
  -e POSTGRES_USER=sally \
  -e POSTGRES_PASSWORD=softKitty \
  -e POSTGRES_DB=app \
  postgres:16.0-alpine3.18


# Now restart the dockerd or reboot your machine
# Check postgres data you loosed it
# 🙈 Everytime I can run migration isn't tolerable
```

#### Bind mount example

```shell
# 1. Create a directory inside postgres data persist. In this case I am using pg_data you can give any name.
mkdir pg_data

# 2. Create the container using bind mount
docker run --name postgres --rm \
  -e POSTGRES_USER=sally \
  -e POSTGRES_PASSWORD=softKitty \
  -e POSTGRES_DB=app \
  -p 5432:5432 \
  -v "${PWD}/pg_data:/var/lib/postgresql/data" \
  postgres:16.0-alpine3.18

# 3. Connect to postgresql
# 3.1 Created the table for demo

# 4. Remove container
docker kill postgres

# 5. Removing the container
docker rm postgres

# 6. Again create the container with attached volume
docker run --name postgres --rm \
  -e POSTGRES_USER=sally \
  -e POSTGRES_PASSWORD=softKitty \
  -e POSTGRES_DB=app \
  -p 5432:5432 \
  -v "${PWD}/pg_data:/var/lib/postgresql/data" \
  postgres:16.0-alpine3.18

# Connect & Ensure you will find tables which you have created in past.
```

#### Named volume example

```shell
# 1. Create a volume name with pg_data you can give any name
docker volume create pg_data

# 2. Create an postgres with same name
docker run --name postgres --rm \
  -e POSTGRES_USER=sally \
  -e POSTGRES_PASSWORD=softKitty \
  -e POSTGRES_DB=app \
  -p 5432:5432 \
  -v "pg_data:/var/lib/postgresql/data" \
  postgres:16.0-alpine3.18

# 3. Connect to postgresql
# 3.1 Created the table for demo

# 4. Remove container
docker kill postgres

# 5. Removing the container
docker rm postgres

# 6. Again create the container with attached volume
docker run --name postgres --rm \
  -e POSTGRES_USER=sally \
  -e POSTGRES_PASSWORD=softKitty \
  -e POSTGRES_DB=app \
  -p 5432:5432 \
  -v "pg_data:/var/lib/postgresql/data" \
  postgres:16.0-alpine3.18

# Connect & Ensure you will find tables which you have created in past.
```
