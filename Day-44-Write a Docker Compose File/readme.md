
### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

The Nautilus application development team shared static website content that needs to be hosted on the httpd web server using a containerised platform. The team has shared details with the DevOps team, and we need to set up an environment according to those guidelines. Below are the details:

1. On App Server 3 in Stratos DC create a container named `httpd` using a docker compose file `/opt/docker/docker-compose.yml` (please use the exact name for file).
2. Use `httpd` (preferably `latest` tag) image for container and make sure container is named as `httpd`; you can use any name for service.
3. Map `80` number port of container with port `5002` of docker host.
4. Map container's `/usr/local/apache2/htdocs` volume with `/opt/security` volume of docker host which is already there. (please do not modify any data within these locations).



# Solution :- 


1. Login to the server (do it by yourself)

2. Navigate to the directory and then create a file named `docker-compose.yml`

  ``` bash
      cd /opt/docker
      vi docker-compose.yml
  ```

  - Paste the following content to the file you created

  ``` text

    services:
      httpd:
        container_name: httpd
        image: httpd:latest
        ports:
          - "5002:80"
        volumes:
          - /opt/security:/usr/local/apache2/htdocs

  ```

  - Do checkout the file ![compose file](./docker-compose.yml) for indentation

3. Make the container up and running and then verify the container 

  ``` bash
      docker compose up -d 
      docker ps -a
  ```

4. Verify the container is serving the static website

  ```bash
    curl localhost:5002
  ```





