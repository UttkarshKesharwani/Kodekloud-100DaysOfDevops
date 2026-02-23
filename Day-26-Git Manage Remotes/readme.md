
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The xFusionCorp development team added updates to the project that is maintained under `/opt/demo.git` repo and cloned under `/usr/src/kodekloudrepos/demo`. Recently some changes were made on Git server that is hosted on Storage server in Stratos DC. The DevOps team added some new Git remotes, so we need to update remote on `/usr/src/kodekloudrepos/demo` repository as per details mentioned below:

1. In `/usr/src/kodekloudrepos/demo` repo add a new remote `dev_demo` and point it to `/opt/xfusioncorp_demo.git` repository.
2. There is a file `/tmp/index.html` on same server; copy this file to the repo and add/commit to master branch.
3. Finally push master branch to this new remote origin.

# Soltuion :- 

1. Login to the storage server (do it by yourself) and then switch to the root user

2. Move to the directory.

  ``` bash 
     cd /usr/src/kodekloudrepos/demo
  ```
3. check the remote origin 
 
  ``` bash 
    git remote -v
    git branch
  ``` 

4. Add new remote and then check if it's added or not

   ```sh
    git remote add dev_demo /opt/xfusioncorp_demo.git
    git remote -v
  ```

5  Copy file and commit changes

    ```bash
      cp /tmp/index.html /usr/src/kodekloudrepos/demo
      git add .
      git commit -m "added index.html file"
    ```

6. Now, Push the changes to dev_beta remote

    ```bash
    git push dev_demo master
    ```