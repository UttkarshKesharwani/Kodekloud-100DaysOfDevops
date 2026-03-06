
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus DevOps team possesses confidential data on App Server 3 in the Stratos Datacenter. A container named ubuntu_latest is running on the same server.
1. Copy an encrypted file `/tmp/nautilus.txt.gpg` from the docker host to the `ubuntu_latest` container located at `/usr/src/`. Ensure the file is not modified during this operation.

# Things to know :-

1. `docker cp` command :- This command is used to copy the file from host to container , vice-versa , or b/w the containers .

  The general syntax has two main forms:

  - Copying from `Host` to `Container`:
      ``` bash
      docker cp [OPTIONS] SRC_PATH CONTAINER:DEST_PATH
      ```

      eg:- `docker cp ./myfile.txt mycontainer:/tmp/myfile.txt`


  - Copying from `Container` to `Host`:
      ``` bash
      docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH
      ```

      eg :- `docker cp mycontainer:/etc/hostname ./hostname.txt`

2. Importance of this command :- Sometimes sensitive configuration files, certificates, or encrypted data must be moved into containers during deployments. Knowing how to securely transfer files between the host and containers is an important DevOps skill.

# Solution :-

1. Login to the app server 

2. Copy the file from the host to docker container

  ``` bash
    docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/usr/src/
  ```

3. Verfiy it using going inside the docker container

  ``` bash 
      docker exec -it <container_name or id> bash
  ```

  then, you will reached inside the docker conatiner now verify the file using the `ls` command 

  `ls /usr/src`

