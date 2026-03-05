


### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus DevOps team is conducting application deployment tests on selected application servers. They require a nginx container deployment on Application Server 2. Complete the task with the following instructions:
1. On Application Server 2 create a container named `nginx_2` using the `nginx` image with the `alpine` tag. Ensure container is in a `running` state.

# Solution :- 

1. Login to the server 

2. Install and run nginx 

  ``` bash 
    docker run -p 80:80 -d --name nginx_2 nginx:apline
  ```

3. Verify it 

  ``` bash
    curl http://localhost:80
  ``` 
  
  You will se the nginx default page


