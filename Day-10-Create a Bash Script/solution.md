

# Do follow for more such content
Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 2 in Stratos Datacenter, and they need to create a bash script named official_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 2).

1. Create a zip archive named xfusioncorp_official.zip of /var/www/html/official directory.
2. Save the archive in /backup/ on App Server 2. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.
3. Copy the created archive to Nautilus Backup Server server in /backup/ location.
4. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.
5. Do not use sudo inside the script.

Note:
The zip package must be installed on given App Server before executing the script. This package is essential for creating the zip archive of the website files. Install it manually outside the script.




# Solution

The very first step , login to your server given in the question (do it by yourself)

1. Step-1 :- Install zip utility because it doesnt come by default 
    `sudo dnf install zip`

2. Step-2 :- Create a new ssh key by using command below :-
    `ssh-keygen -t rsa` , this will create a public/private key inside your(~/.ssh/) directory

3. Step-3 :- Copy public key generate by the above command , to the "Nautilus Backup Server".
    `ssh-copy-id clint@172.16.238.16`

    > The above step-2 and step-3 lets you genearate and then send the public key to the other server so that i will not ask for password once you transfer the zip file to the "Nautilus Backup Server". 

4. Step-4 :- Go to the `/scripts` directory
    `cd /scripts`

5. Step:-5 :- Make a script file ,asked in your question `official_backup.sh`(in my question)
    `vi official_backup.sh`

6. Step:-6 :- Change the file permission to executable file 
    `chmod 744 official_backup.sh`

7. Step:-7 :- Write command in the script file, given in your question
    `zip -r /backup/xfusioncorp_official.zip  /var/www/html/official`
    `scp /backup/xfusioncorp_official.zip clint@172.16.238.16:/backup/`
  
8. Step:-8 :- Run your `official_backup.sh` once to check all goes well.



# Things to know:-

1. There are two ways to login/authenticate you server 

   - password :- In this case , every time you try to login the server will ask the password

   - password-less :- In this case, you machine has the private key and your server has the public key , whenever you login it tries to match your public-private key. Whenever you tries to connect the remote server to remote server(basically between two remote server) either it will ask for password or you have to exchange the private-public key between the server. 
   So, here the two commands `ssh-keygen`(it create the public and private key into your current system in the `~/.ssh/` directory) & `ssh-copy-id`(lets you send the public key from your current login machine to the other remote host) comes into existence.
