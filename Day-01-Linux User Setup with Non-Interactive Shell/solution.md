
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


<h2>Moving Ahead to the solution</h2>

Before moving to the solution first understand ,how we prevent access the user(system user) to prevent login. When we create a user, the linux gives the shell access to that user by default and the binary executable file present in "/bin/bash".
Simlarly, to prevent the login or shell or ssh access to the user , the binary executble file is present int "/sbin/nologin".


<h2>Moving to the command</h2>

man useradd :- This command gives you the manual , how to add the user ?

useradd [options] username :- this command helps you to add the user

![alt text](image.png) :- this image is screen shot of manual 

-s is option which accept argument(path to the qshell -> /sbin/nologin  in this case)


<h2>Final Answer</h2>

1. First, login into the app server using `SSH`:

    ```sh
    ssh user@app-server-ip or ssh user@server-name
    ```

    > It will ask for user password, enter the correct password.

2. After login into server, run the following command to create user with non-interactive shell

    ```sh
    sudo useradd -m -s /usr/sbin/nologin user-name
    ```

    `s`: for shell, here we are giving nologin shell

    `m`: for user home directory, It will create a directory with user-name under /home

3. Verify the result

    ```sh
    cat /etc/passwd
    ```

    It should give you a list of users where you will find your created user. It will look like this:
    `yousuf:x:1003:1004::/home/yousuf:/usr/sbin/nologin`

    Try to login using:

    ```sh
    sudo su user-name
    ```

    Output: `This account is currently not available.`


### useradd Command Options

- `-m`: Create home directory
- `-s`: Specify shell
- `-d`: Custom home directory path
- `-g`: Primary group
- `-G`: Additional groups
- `-e`: Account expiry date


