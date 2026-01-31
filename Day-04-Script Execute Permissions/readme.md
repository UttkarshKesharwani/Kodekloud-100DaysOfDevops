# Do follow for more such content
Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/

# Problem Statement :- 
In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 1 within the Stratos Datacenter.
> Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 1. Additionally, ensure that all users have the capability to execute it.

# Think to know

You shoud know what is the permissions(for the folder/file) in linux
-> we use `chmod [options] mode file` command 

- Lets understand what does `mode` here:-
  - Suppose you made a folder or file in linux server, since the user support multi user at once and you want/forbid the 
    user to give access/deny to the folder/file you created for read or write or execute. So here permission comes into the picture 
  - `r` -> means read , r equals to 4 . Don't panic we will learn why we are giving some values to read , write and execute
  - `w` -> means write , w equals to 2
  - `e` -> execute (just like you run the programme file like java, cpp file etc.) , e equal to 1

- Now, how we can check what our current file/folder have permissions

  -`ls -l` :- to list the file in the long list format(basically detailed view)

  👉 This command shows files in long list format (detailed view).
  > -rw-r--r-- 1 root root 1234 Jan 30 xfusioncorp.sh

1. Now, understand what does `-rw-r--r--` here ?

  Lets, break down this into few section 
    - The first word decide , this file is directory or file 
      `-` -> if this is the first character then this is `file`
      `d` -> if this the first character start with `d` then this is directory(folder) 
    - Now we left over with `rw-r--r--` .
      Again we are going to divide this 9 words into 3 parts like `rw-`,`r--`,`r--` in this case.
      - `rw-` -> this thing defines the overall permission for the user that create the file or directory , here in this case it has access to read(r),write(w) only and the `-` here defined that not have permission to execute, similary applicable for the below point
      - `r--` -> this thing defines the overall permission for the group of users that belongs to one group , only read(r) permission is given
      - `r--` -> this permission defines the overall persmission given to the third user(like there exist a lot of user in one server) , only read(r) permission is given , means only he can read not write or execute

2. Understanding by taking example 
  
    suppose you want to give access for read(4), or write(2) or execute(1). to any other the user , means -> user, groups , other users , then you just need to sum up whichever persmission you want to give
      - suppose ,if you want to give the read, write , execute permission to  other user present in you server , then you can just need to add `4+2+1` 
      - Simlarly for the users  or groups also


eg :- chmod 777 file.txt , here 7 -> means -> read(r) , write(w) , execute(e) for every triplets
  




