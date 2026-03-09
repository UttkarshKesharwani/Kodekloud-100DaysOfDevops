### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

One of the Nautilus DevOps team members was working to configure services on a kkloud container that is running on App Server 3 in Stratos Datacenter. Due to some personal work he is on PTO for the rest of the week, but we need to finish his pending work ASAP. Please complete the remaining work as per details given below:

1. Install `apache2` in `kkloud` container using `apt` that is running on App Server 3 in Stratos Datacenter.
2. Configure Apache to listen on port `8089` instead of default `http` port. Do not bind it to listen on specific IP or hostname only, i.e it should listen on localhost, 127.0.0.1, container ip, etc.
3. Make sure Apache service is up and running inside the container. Keep the container in running state at the end.

# Solution :-

1.  Login and Connect to App Server 3 (do it by yourself)

    ```bash
    ssh banner@stapp03
    ```

2.  Check Running Containers

    ``` bash
        docker ps
    ```
3. Enter inside the Container

    ```bash
      docker exec -it kkloud bash
    ```
4. Update Package List and Install Apache2

    ```bash
      apt update && apt install apache2 -y
    ```

5. Start and Verify Apache Service

    ```bash
      service apache2 start && service apache2 status
    ```

6. Test Apache befor changing the port (Default Port 80)

    ``` bash
        curl localhost
            or
        curl 127.0.0.1
    ```
Expected: Apache default page HTML.

7. Change Apache Listening Port to 8089 and then Update Virtual Host Configuration

    ``` bash
      sed -i 's/Listen 80/Listen 8089/g' /etc/apache2/ports.conf 
      sed -i 's/*:80/*:8089/g' /etc/apache2/sites-available/000-default.conf 
    ```

8. Restart Apache

  ```bash
    service apache2 restart
  ```

9. Test Apache on New Port

    ``` bash
        curl localhost:8089
            or
        curl 127.0.0.1:8089
    ```