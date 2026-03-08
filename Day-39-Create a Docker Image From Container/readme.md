
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

One of the Nautilus developer was working to test new changes on a container. He wants to keep a backup of his changes to the container. A new request has been raised for the DevOps team to create a new image from this container. Below are more details about it:

1. Create an image `official:devops` on Application Server 2 from a container `ubuntu_latest` that is running on same server.



# Things to know:-  

1. If you already have a running container and want to create a new Docker image from it, you can use the docker commit command.

=> This is useful when:
- You manually installed packages inside a container
- You changed configurations
- You want to save the current state as an image

Syntax :- `docker commit <container_id_or_name> <new_image_name>:<tag>`
eg :- `docker commit my-container myimage:v1`

This creates a new image called `myimage:v1` from the running container `my-container`.


# Solution :-

1. Login to the server 

2. Create image from the running container

  ``` bash
      docker commit 1523a73a6ae3 official:devops  
  ```

3. Verify the images

  ``` bash
    docker images
  ```
you will see the new images that you created 