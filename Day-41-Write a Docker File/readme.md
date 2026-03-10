
### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-
As per recent requirements shared by the Nautilus application development team, they need custom images created for one of their projects. Several of the initial testing requirements are already been shared with DevOps team. Therefore, create a docker file `/opt/docker/Dockerfile` (please keep D capital of `Dockerfile`) on App server 1 in Stratos DC and configure to build an image with the following requirements:

1. Use `ubuntu:24.04` as the base image.
2. Install `apache2` and configure it to work on `8088` port. (do not update any other Apache configuration settings like document root etc).


# Solution :-

1. Login to the server and switch to the root user

2. Navigate to the directory and then create a Dockerfile

    ```bash
      cd /opt/docker
      vi Dockerfile
    ```

3. Paste the content below in the Dockerfile

    ``` text

        FROM ubuntu:24.04

        RUN apt-get update && \
            apt-get install -y apache2 && \
            sed -i 's/80/8088/g' /etc/apache2/ports.conf && \
            sed -i 's/*:80/*:8088/g' /etc/apache2/sites-available/000-default.conf

        EXPOSE 8088

        CMD ["apachectl", "-D", "FOREGROUND"]

    ``` 

4. Build the image and then verify the image

  ``` bash
      cd /opt/docker
      docker build -t custom-apache .
      docker images
  ```

5. Run the container and then verify the running container

  ``` bash
      docker run -d -p 8088:8088 custom-apache
      docker ps
  ```

6. verify using the curl command from inside the app server

  ```bash
    curl http://localhost:8088
  ```


  