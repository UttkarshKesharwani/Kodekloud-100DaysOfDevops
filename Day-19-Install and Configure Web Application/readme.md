

### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-
xFusionCorp Industries is planning to host two static websites on their infra in Stratos Datacenter. The development of these websites is still in-progress, but we want to get the servers ready. Please perform the following steps to accomplish the task:

1. Install `httpd` package and dependencies on `app server 3`.
2. Apache should serve on port `5000`.
3. There are two website's backups `/home/thor/blog` and `/home/thor/apps` on jump_host. Set them up on Apache in a way that blog should work on the link `http://localhost:5000/blog/` and apps should work on link `http://localhost:5000/apps/` on the mentioned app server.
4. Once configured you should be able to access the website using curl command on the respective app server, i.e curl `http://localhost:5000/blog/` and curl h`ttp://localhost:5000/apps/`


# Solution :- 

1. Login to the app server .

2. Install and configure and then restart `httpd` service

  ```sh
    sudo yum install -y httpd
  ```
  Run the following command 

  ``` bash
    sudo cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.bak
    sudo sed -i 's/80/5000/g' /etc/httpd/conf/httpd.conf 
  ```

  `/etc/httpd/conf/httpd.conf` :- place in centos where the configration file for httpd is stored
  - By default httpd uses port `80` so we use `sudo sed -i 's/80/5000/g' /etc/httpd/conf/httpd.conf ` this command to change the port from `80` to `5000` in my case.

  ``` bash 
      sudo yum restart httpd
  ```

3. Verify the port by running ss(socket statistic)/netstat(network statics) command 

  ``` text
    [root@stapp03 conf]# ss -tulpn | grep 5000
    tcp   LISTEN 0      511          0.0.0.0:5000       0.0.0.0:*    users:(("httpd",pid=5395,fd=3),("httpd",pid=5394,fd=3),("httpd",pid=5393,fd=3),("httpd",pid=5385,fd=3))
    [root@stapp03 conf]# 
  ```
  Use can clearly see ,now httpd service running on port `5000` 


4. Copy the source code from jump host to the app server

   ``` bash
    scp -r /home/thor/blog banner@stapp03:/home/banner
    scp -r /home/thor/apps banner@stapp03:/home/banner
  ```

5. Thing to know before moving to this step

  `DocumentRoot` :- It means from where the httpd service take your/serve file. It is the place where we put our website . Httpd service use `/var/www/html` path by default (you can change from which folder you want to serve your file to the internet , if you do so then you need to change the httpd configration file i.e, `/etc/httpd/conf/httpd.conf`).

  - Now place the website in the DocumentRoot folder.

    ```sh
      sudo cp -r /home/banner/apps /var/www/html/
      sudo cp -r /home/banner/blog /var/www/html
    ```

6. Restart `httpd` sevice

7. Verify the result , by running the command within the same app server 
  
    ```sh
      curl http://localhost:5000/apps/
      curl http://localhost:5000/blog/
    ```


# Things to Know 

1. Apache serves folders automatically inside DocumentRoot. So when you open: http://server-ip:5000/apps/ then , Apache internally looks for: /var/www/html/apps/index.html , because of `DirectoryIndex index.html` is present in the config file . 
  - Apache is `filesystem-driven`. Meaning: URL structure = directory structure . If folder exists → Apache serves it.


2. Nginx usually needs explicit `location` blocks when you want custom behavior.
    
    - In Nginx, you normally write:

    ``` text 
      location /apps {
        root /var/www/html;
      }
    ```

    because Nginx is `request-routing driven`, not filesystem-driven.Nginx expects you to define how requests should be handled.