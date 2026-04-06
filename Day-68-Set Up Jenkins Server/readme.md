### Do follow for more such content

### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :-

The DevOps team at xFusionCorp Industries is initiating the setup of CI/CD pipelines and has decided to utilize Jenkins as their server. Execute the task according to the provided requirements:

1. Install Jenkins on the jenkins server using the `apt` utility only, and start it using the `service` command.
   If you face a timeout issue while starting the Jenkins service, first check the service status with `service jenkins status`
   Then review the logs in `/var/log/jenkins/jenkins.log` to identify the cause.
2. Jenkin's admin user name should be `theadmin`, password should be `Adm!n321`, full name should be `Ammar` and email should be `ammar@jenkins.stratos.xfusioncorp.com`.

Note:

1. To access the `jenkins` server, connect from the jump host using the `root` user with the password `S3curePass`.
2. After Jenkins server installation, click the Jenkins button on the top bar to access the Jenkins UI and follow on-screen instructions to create an admin user.

# Solution :-

1.  Jenkins required the java so we need to install the java first

        ``` bash
            apt update
            apt install openjdk-17-jdk -y
        ```

2. Add Jenkins repo

        ``` bash
          wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian/jenkins.io.key
          echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/" > /etc/apt/sources.list.d/jenkins.list
          apt update
        ```
3. Install Jenkins, start and then verify the jenkis

        ``` bash    
          apt install jenkins -y
          service jenkins start 
          service jenkins start
        ```

4. UI SETUP -> click the jenkins button 

  Run command to generate the pass and then paste into the browser 
  > cat /var/lib/jenkins/secrets/initialAdminPassword

  click on the :- Install suggested plugins

5. Create Admin User

    ``` text
        Username: theadmin
        Password: Adm!n321
        Confirm: Adm!n321
        Full Name: Ammar
        Email: ammar@jenkins.stratos.xfusioncorp.com
    ```