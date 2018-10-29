Redis, RE-dis is an open-source in-memory data structure project implementing a distributed, in-memory key-value database with optional durability

This article is something I learn when wanted to use redis without polluting the local machine with redis installation.
The first thing came to my mind is to use ```Docker```. So lets begin 

1. Get the official redis docker image
Run the following command
```
docker pull redis
```
Note: you can refer to official redis docker repository [here](https://hub.docker.com/_/redis/)

2. Check the downloaded redis image
Run the following command to see all the locally available docker images.
```
docker images
```
you will see something like this as result of above command<br/>
![alt text](https://github.com/saurabhdeshpande49/redis-docker/blob/master/docker_images.jpg)

3. Lets create a redis.conf file 
You can download a sample redis.conf file from [here](http://download.redis.io/redis-stable/redis.conf)

4. Run the docker image 
Before doing this lets create a local volume where the redis.conf is available and mount it in the docker image while 
running it. e.g/ /home/<your-user-name>/redis/redis.conf

Run the below command to run the redis docker image as demon.
```
docker run -d -v /home/saurabh/redis/redis.conf:/usr/local/etc/redis/redis.conf -p 6379:6379 --name myredis redis
```
You can now inspect the currently running docker image using following command

```
docker exec -it myredis bash

//the above command will take you inside the container 
root@e42647bf2a4e:/data#
```
To test weather the redis is working or not lets connect to it through redis-cli
run the following command inside the container
```
root@e42647bf2a4e:/data# redis-cli -h localhost -p 6379 -a <password-from-redis.conf-file>
localhost:6379> // you are in now test the redis 
localhost:6379> ping
PONG
```

Your redis container is working fine. Now you can connect to this redis instance(PORT 6379) from any application on your machine.
