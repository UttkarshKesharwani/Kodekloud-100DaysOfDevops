
### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-
The Nautilus DevOps team is planning to host an application on a nginx-based container. There are number of tickets already been created for similar tasks. One of the tickets has been assigned to set up a nginx container on Application Server 2 in Stratos Datacenter. Please perform the task as per details mentioned below:
a. Pull nginx:alpine docker image on Application Server 2.
b. Create a container named apps using the image you pulled.
c. Map host port 3004 to container port 80. Please keep the container in running state.

# Why this matters :-

- Docker container runs on isolated enviroment, its means external traffic cannot communicate with the running container , so here the port mapping with the host machine comes into picture , that lets you talk to the contianer whenever any request coming to your host machine with the port you configured will route to the running container.

# Solution:- 

1. Login to the server(do it by yourself)

2. Install the `nginx:alpine` image with name `apps` and port mapping `3004`

  ``` bash
      docker run -p 3004:80 -d --name apps nginx:alpine
  ```

3. Verify the running container

  ``` bash
    docker ps -a
  ```

  you will see like-  

  ``` text
    CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                   NAMES
    e1c20c73d0d3   nginx:alpine   "/docker-entrypoint.…"   7 seconds ago   Up 6 seconds   0.0.0.0:3004->80/tcp, :::3004->80/tcp   apps
    [steve@stapp02 ~]$ 
  ```




