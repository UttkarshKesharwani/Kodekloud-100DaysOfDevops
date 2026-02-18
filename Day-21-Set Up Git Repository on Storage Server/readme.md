

### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus development team has provided requirements to the DevOps team for a new application development project, specifically requesting the establishment of a Git repository. Follow the instructions below to create the Git repository on the Storage server in the Stratos DC:

1. Utilize yum to install the `git` package on the Storage Server.
2. Create a bare repository named `/opt/blog.git` (ensure exact name usage).


# Solution :-


1. Login to Storage Server and Install git

    ```sh
    sudo yum update -y
    sudo yum install -y git
    ```

2. Create a bare repository

    ```sh
   sudo git init --bare /opt/demo.git
   ```

