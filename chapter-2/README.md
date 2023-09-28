#### Chapter 2

In this chapter you will learn:

- How to build a simple OCI image

```shell
# 1. Create a sample shell script
cat <<EOF >soft-kitty.sh
#!/bin/sh
echo "Soft kitty,\n
Warm kitty,\n
Little ball of fur,\n
Happy kitty,\n
Sleepy kitty,\n
Purr purr purr."
EOF

#2. Writting a Dockerfile
cat <<EOF >Dockerfile
# You can use scratch as base image
FROM alpine
WORKDIR /app
COPY . .
CMD ["/bin/sh", "soft-kitty.sh"]
EOF

# 3. Build the image
docker build -t soft-kitty:v1 .

# 4. Run the image
docker run --rm --name=soft-kitty soft-kitty:v1

# 5. [Optional] You can push the image to a registry
docker tag soft-kitty:v1 bhtk/soft-kitty:v1

# 5.1 Image push
docker push bhtk/soft-kitty:v1
```
