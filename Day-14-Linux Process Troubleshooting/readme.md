
# Problem Statement :-

The production support team of xFusionCorp Industries has deployed some of the latest monitoring tools to keep an eye on every service, application, etc. running on the systems. One of the monitoring systems reported about Apache service unavailability on one of the app servers in Stratos DC.

Identify the faulty app host and fix the issue. Make sure Apache service is up and running on all app hosts. They might not have hosted any code yet on these servers, so you don’t need to worry if Apache isn’t serving any pages. Just make sure the service is up and running. Also, make sure Apache is running on port `5003` on all app servers.

# Thing to know before proceeding to the solution :-

- `netstat -tulpn` :- It is a command used to see network connections and listening ports on a system . In simple words:netstat shows which ports are open and which services are using them.
- `telnet ip [port]` :- The primary purpose of the telnet command is to establish a connection to a remote host on a specific port . Earlier it was used to login the remote host , but we generally dont use now a days because the login and password are being sent as plain text , which hacker might intercept so use `ssh` nowadays. Telnet service runs on port `23`.


# Solutions 

Steps :- 

1. You have two ways to check which app service is not running the apache server 
    - try login each server one by one then check the service is running on not using the command `sudo systemctl status httpd`
    - try connect the remote server on a specific port using the command `telnet stapp01 5003` and do for the other app server , the server which refused the connection that server will have the problem on running httpd service , so try to login on that server only using `ssh`.
   
2.  Check `httpd/apache/nginx` service status using 
    > sudo systemctl status httpd

    ``` shell
      [root@stapp01 ~]# systemctl status httpd
      ● httpd.service - The Apache HTTP Server
        Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
        Active: failed (Result: exit-code) since Wed 2026-02-11 07:31:38 UTC; 14min ago
          Docs: man:httpd(8)
                man:apachectl(8)
        Process: 809 ExecStop=/bin/kill -WINCH ${MAINPID} (code=exited, status=1/FAILURE)
        Process: 808 ExecStart=/usr/sbin/httpd $OPTIONS -DFOREGROUND (code=exited, status=1/FAILURE)
      Main PID: 808 (code=exited, status=1/FAILURE)

      Feb 11 07:31:37 stapp01.stratos.xfusioncorp.com systemd[1]: Starting The Apache HTTP Server...
      Feb 11 07:31:37 stapp01.stratos.xfusioncorp.com httpd[808]: (98)Address already in use: AH00072...3
      Feb 11 07:31:37 stapp01.stratos.xfusioncorp.com httpd[808]: no listening sockets available, shu...n
      Feb 11 07:31:37 stapp01.stratos.xfusioncorp.com httpd[808]: AH00015: Unable to open logs
      Feb 11 07:31:37 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: main process exited,...E
      Feb 11 07:31:38 stapp01.stratos.xfusioncorp.com kill[809]: kill: cannot find process ""
      Feb 11 07:31:38 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: control process exit...1
      Feb 11 07:31:38 stapp01.stratos.xfusioncorp.com systemd[1]: Failed to start The Apache HTTP Server.
      Feb 11 07:31:38 stapp01.stratos.xfusioncorp.com systemd[1]: Unit httpd.service entered failed s....
      Feb 11 07:31:38 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service failed.
      Hint: Some lines were ellipsized, use -l to show in full.
    ```

We can clearly see the problem that port is already is being used 

  ``` text

        Feb 11 07:31:37 stapp01.stratos.xfusioncorp.com httpd[808]: (98)Address already in use: AH00072...3
        Feb 11 07:31:37 stapp01.stratos.xfusioncorp.com httpd[808]: no listening sockets available, shu...n
  ```

3. Check which service is using which port using command 

  > netstat -tulnp
  
  ``` shell
    [root@stapp01 ~]# netstat -tulnp
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
    tcp        0      0 127.0.0.11:43987        0.0.0.0:*               LISTEN      -                   
    tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      1/init              
    tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      504/sshd            
    tcp        0      0 127.0.0.1:5003          0.0.0.0:*               LISTEN      783/sendmail: accep 
    tcp6       0      0 :::111                  :::*                    LISTEN      507/rpcbind         
    tcp6       0      0 :::22                   :::*                    LISTEN      504/sshd            
    udp        0      0 127.0.0.11:60018        0.0.0.0:*                           -                   
    udp        0      0 0.0.0.0:111             0.0.0.0:*                           1/init              
    udp        0      0 0.0.0.0:665             0.0.0.0:*                           507/rpcbind         
    udp6       0      0 :::111                  :::*                                507/rpcbind         
    udp6       0      0 :::665                  :::*                                507/rpcbind 
    
  ```

  We can see that port `5003` is already being used by sendmail process , so change the port of the sendmail

4. Change the configration file for the sendmail 
  ```bash
    cd /etc/mail
    vi sendmail.mc
    ```
  Try to find:-

  > DAEMON_OPTIONS(`Port=5003,Addr=127.0.0.1, Name=MTA')dnl

  and change the port from 5003 to any other port lets say 5004

5. Restart the both service

  ``` bash
    sudo systemctl restart httpd sendmail
  ``` 

6. Verify it agian by running `netstat -tulnp`

  ``` text
      [root@stapp01 mail]# netstat -tulnp
      Active Internet connections (only servers)
      Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
      tcp        0      0 0.0.0.0:5003            0.0.0.0:*               LISTEN      921/httpd           
      tcp        0      0 127.0.0.11:43987        0.0.0.0:*               LISTEN      -                   
      tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      1/init              
      tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      504/sshd            
      tcp        0      0 127.0.0.1:5004          0.0.0.0:*               LISTEN      908/sendmail: accep 
      tcp6       0      0 :::111                  :::*                    LISTEN      507/rpcbind         
      tcp6       0      0 :::22                   :::*                    LISTEN      504/sshd            
      udp        0      0 127.0.0.11:60018        0.0.0.0:*                           -                   
      udp        0      0 0.0.0.0:111             0.0.0.0:*                           1/init              
      udp        0      0 0.0.0.0:665             0.0.0.0:*                           507/rpcbind         
      udp6       0      0 :::111                  :::*                                507/rpcbind         
      udp6       0      0 :::665                  :::*                                507/rpcbind 
  ``` 