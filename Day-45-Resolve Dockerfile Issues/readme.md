

### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

The Nautilus DevOps team is working to create new images per requirements shared by the development team. One of the team members is working to create a `Dockerfile` on App Server 2 in Stratos DC. While working on it she ran into issues in which the docker build is failing and displaying errors. Look into the issue and fix it to build an image as per details mentioned below:

a. The Dockerfile is placed on App Server 2 under `/opt/docker` directory.
b. Fix the issues with this file and make sure it is able to build the image.
c. Do not change base image, any other valid configuration within `Dockerfile`, or any of the data been used — for example, `index.html`.


Note: Please note that once you click on FINISH button all the existing containers will be destroyed and new image will be built from your Dockerfile.


# Solution :-
 
1. Login to the app server 

2. Navigate the directory and then edit the Dockerfile

  ``` bash
      cd /opt/docker
      vi Dockerfile
  ```

  now , replace the docker file with the given text

  ``` text

    FROM httpd:2.4.43

    RUN sed -i "s/Listen 80/Listen 8080/g" /usr/local/apache2/conf/httpd.conf

    RUN sed -i '/LoadModule\ ssl_module modules\/mod_ssl.so/s/^#//g' /usr/local/apache2/conf/httpd.conf

    RUN sed -i '/LoadModule\ socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//g' /usr/local/apache2/conf/httpd.conf

    RUN sed -i '/Include\ conf\/extra\/httpd-ssl.conf/s/^#//g' /usr/local/apache2/conf/httpd.conf

    COPY certs/server.crt /usr/local/apache2/conf/server.crt

    COPY certs/server.key /usr/local/apache2/conf/server.key

    COPY html/index.html /usr/local/apache2/htdocs/

  ```

3. Now build and verify the image 

  ``` bash
    docker build -t httpd-ssl .
    docker images
  ```
  