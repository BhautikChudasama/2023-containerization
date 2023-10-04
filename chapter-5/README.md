#### Chapter 4

In this chapter you will learn:

- How `docker-compose` abstract above lessons and simplify container orchestration.

```shell
# If you are following from chapter 1, please remove the existing running in order to create the same name container.

# [Optional] I am using 🙈 kill but for graceful shut down please use stop
docker kill postgres
docker rm postgres

# Docker-compose
# Before starting make sure you have docker-compose installed
# 1. Create docker-compose.yml
cat <<EOF >docker-compose.yaml
version: '3.8'
services:
  postgres:
    image: postgres:16.0-alpine3.18
    container_name: postgres
    environment:
      POSTGRES_USER: sally
      POSTGRES_PASSWORD: softKitty
      POSTGRES_DB: app
    networks:
      - app-network

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin
    ports:
      - "8080:80"
    networks:
      - app-network

networks:
  app-network:
    driver: bridge
EOF

# 2. Start the services.
docker-compose up -d

# [Optional] Check the services are running.
docker ps

# 3. Stop, and Remove the services.
docker-compose down
```
### Learn by Doing

In this section you can apply the knowledge by doing hands-on exercises:

1. Can you add persistence to this chapter?
