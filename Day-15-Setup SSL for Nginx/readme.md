# Do follow for more such content
Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-
The system admins team of xFusionCorp Industries needs to deploy a new application on `App Server 1` in Stratos Datacenter. They have some pre-requites to get ready that server for application deployment. Prepare the server as per requirements shared below:



1. Install and configure `nginx` on `App Server 1`.
2. On App Server 1 there is a self signed SSL certificate and key present at location `/tmp/nautilus.crt` and `/tmp/nautilus.key`. Move them to some appropriate location and deploy the same in Nginx.
3. Create an index.html file with content Welcome! under Nginx document root.
4. For final testing try to access the App Server 1 link (either hostname or IP) from jump host using curl command. For example curl -Ik https://<app-server-ip>/



# Things to Know :-

1. `ssl` certificate :- SSL (now technically called TLS) certificate is used to , encrypt communication between client and server. When you open any webstie using `https` instead of `http` , the b/w client and server is encrypted. So nobody in between can read: passwords,API data, cookies, payment info etc.

2. Need of `ssl` certificate ? :- Without SSL the data b/w client and server is not encrypted hacker might intercept it.

3. Internals Structure of `ssl` certificate :- 
  An SSL certificate is just a digital file containing - 
    - Domain name :- represent that the particular certificate is valid only for this domain.
    - Public Key :- Used for encryption. Server keeps  Public key (inside certificate) and Private key (secretly) both
    - Certificate Authority (CA) :- Organization that issued certificate , eg- Let's Encrypt, DigiCert, GlobalSign. They verify domain ownership.
    - Validity Period :-  After this time frame certificate expires.
    - Digital Signature :- CA signs certificate so browser trusts it.

4. How SSL Works (Behind the Scenes) 
  - When browser connects , Browser asks server that send your certificate
  - Server sends SSL certificate.
  - Browser checks:- Is certificate valid?, Is CA trusted?, Is domain matching?
  - Browser creates session key and encryption starts.

5. Where Do We Configure SSL? 
  Depends on architecture. Usually SSL is configured at Web Server(nginx ,apache) , Load Balancer, Application Level (Less Common)


# Solution :-

1. Log in to the app server given in the problem statement(do it by yourself)
 
2. Install and start nginx 
    
    ``` bash
      sudo yum install nginx -y
      sudo systemctl start nginx
      sudo systemctl enable nginx
    ```

    - verify nginx status using `systemctl status nginx`

3. Move SSL Certificate and Key , SSL files should not remain in /tmp. Move them to a secure location.

    ``` bash
      sudo mkdir -p /etc/nginx/ssl
      sudo mv /tmp/nautilus.* /etc/nginx/ssl/
    ```

    The above command will make the `ssl/` directory and all the files will move inside it.

4. Open the nginx configration file to check the "Nginx document root" (Nginx document root is the directory from where Nginx serves files to users). 
    
    you can see the nginx conf file using the command `sudo vi /etc/nginx/nginx.conf`.

    you will see like
    ``` text
        root /usr/share/nginx/html;
    ```
    means , from here the nginx will serve the file to the internet 

5. Create `index.html`

  Create the default webpage under "nginx document root" using command :

  ``` bash 
    echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html
  ```

6. It is best practice to always make a backup of nginx(or any) configration file before making changes directly to it.

  ``` bash 
      copy /etc/nginx/nginx.conf /etc/nginx/nginx-bkp.conf
  ```

7. Configure `nginx.conf` file for SSL certificate , edit nginx configuration(/etc/nginx/nginx.conf) and enable TLS configuration. 

  open in editor 

  Uncomment the given default configration at the end of the file 

    `ssl_certificate /etc/nginx/ssl/nautilus.crt;` 
    `ssl_certificate_key /etc/nginx/ssl/nautilus.key;`

  add the path 

8. When you try to amend the configration file , you might create a mistake(syntax error) to check that we need to run ``sudo nginx -t` to test the configration file

9. Restart nginx
  ``` bash 
    sudo systemctl reload nginx
  ```

10. Finally test , Test HTTPS connectivity:

 > curl -Ik https://<app-server-ip>/


  

