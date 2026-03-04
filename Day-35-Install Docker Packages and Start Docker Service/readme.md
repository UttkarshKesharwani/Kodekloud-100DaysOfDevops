
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus DevOps team aims to containerize various applications following a recent meeting with the application development team. They intend to conduct testing with the following steps:

1. Install `docker-ce` and `docker compose` packages on `App Server 3`.
2. Initiate the `docker` service.


- Note :- Do checkout:- https://docs.docker.com/engine/install/centos/#os-requirements


# Solution :-

1. Uninstall old versions
  
    ``` bash
        sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
    ```

2. Install using the rpm repository(Set up the repository)
    
    ``` bash
        sudo dnf -y install dnf-plugins-core
        sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    ```

3. Install the docker package 

    ``` bash 
        sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ``` 

4. Start the docker engine

    ``` bash
      sudo systemctl enable --now docker
    ```

5. Verify that the installation is successful by running the hello-world image

    ``` bash 
        sudo docker run hello-world
    ```

