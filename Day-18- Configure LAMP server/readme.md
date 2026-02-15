### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :- 

xFusionCorp Industries is planning to host a WordPress website on their infra in Stratos Datacenter. They have already done infrastructure configuration—for example, on the storage server they already have a shared directory /vaw/www/html that is mounted on each app host under /var/www/html directory. Please perform the following steps to accomplish the task:

1. Install httpd, php and its dependencies on all app hosts.
2. Apache should serve on port `8088 ` within the apps.
3. Install/Configure `MariaDB server` on DB Server.
4. Create a database named kodekloud_db6 and create a database user named `kodekloud_joy` identified as password `LQfKeWWxWD`. Further make sure this newly created user is able to perform all operation on the database you created.
5. Finally you should be able to access the website on LBR link, by clicking on the App button on the top bar. You should see a message like `App is able to connect to the database using user kodekloud_joy`



# Solution :-

1. Login to each app server one by one and install httpd and php with necessary dependency
  
     ```sh
    sudo yum install -y httpd php php-mysqli
    ```

    - now why `php-mysqli` ? . It lets you talk to the database , it acts as a bridge b/w the php and databse(sql/mariadb)

2. Change Apache port and Restart service

    Note :- always take a backup before changing any configration

    ```sh
    sudo cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd-backup.conf
    sudo sed -i 's/\<80\>/8088/g' /etc/httpd/conf/httpd.conf
    sudo systemctl enable --now httpd
    ```

    - now understand `sudo sed -i 's/\<80\>/8088/g' /etc/httpd/conf/httpd.conf` commands do :- 
      here `sed` means stream editor which doesn't open the file in the editor in the interactive way as vi or vim editor does . Instead it will change/edit the file as per your command

3. Verify the port using commad :-
   `sudo ss -tulpn`

   ``` text                                                    
      [root@stapp03 ~]# ss -tulpn | grep 8088
      tcp   LISTEN 0      511          0.0.0.0:8088       0.0.0.0:*    users:(("httpd",pid=3482,fd=3),("httpd",pid=3481,fd=3),("httpd",pid=3480,fd=3),("httpd",pid=3472,fd=3))
  ```

4. Install mariadb-server on Database server

    ```sh
      sudo yum install -y mariadb-server
      sudo systemctl enable --now mariadb
    ```

    verify the mariadb service is up and runnuing

    `sudo systemctl status mariadb | grep "running"`

5. Create User and Database

    ``` bash 
        mysql -u root -e "DROP USER IF EXISTS 'kodekloud_tim'@'localhost';"
        mysql -u root -e "DROP USER IF EXISTS 'kodekloud_tim'@'%';"
        mysql -u root -e "CREATE USER 'kodekloud_tim'@'%' IDENTIFIED BY 'BruCStnMT5';"
        mysql -u root -e "GRANT ALL PRIVILEGES ON kodekloud_db4.* TO 'kodekloud_tim'@'%';"
        mysql -u root -e "FLUSH PRIVILEGES;"
    ```