
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-
The Nautilus application development team has been working on a project repository `/opt/ecommerce.git`. This repo is cloned at `/usr/src/kodekloudrepos` on storage server in Stratos DC. They recently shared the following requirements with the DevOps team:
- There are two branches in this repository, `master` and `feature`. One of the developers is working on the `feature` branch and their work is still in progress, however they want to merge one of the commits from the `feature` branch to the master branch, the message for the commit that needs to be merged into `master` is `Update info.txt`. Accomplish this task for them, also remember to push your changes eventually.

# Things to know :- 

1. Cherry-pick = copy one specific commit from another branch into your current branch Instead of merging whole branch, you pick only one commit. That’s why name is cherry 🍒 pick.

2. Visual understanding

Before:- 
  ``` bash
    main:    M1 —— M2
    feature:        F1 —— F2(bug fix) —— F3
  ``` 
After Run cherry pick → main gets F2 only:

  ``` bash
    main: M1 —— M2 —— F2 
  ```
Feature branch remains unchanged.

3. How to use cherry pick ?
  - Go to the current working branch 
  - Perform `git log` ,then copy commit hash
  - Switch to the branch you want to merge into
  - perform cherry pick `git cherry-pick <commit-hash>`
  - Now push the code `git push origin <branch>`


# Solution :- 

1. Login to the storage server and switch to the root user(do it by yourself)

2. Navigate to the correct directory 

    ``` bash 
      cd /usr/src/kodekloudrepos/ecommerce
    ```

3. Check the current branch and then switch to `feature` branch

    ``` bash 
        git branch
        git checkout feature
    ```

4. Log the commit and copy the hash and then switch the branch you want to merge commit into(master in this case)

    ``` bash 
      git log --oneline
      git checkout master
    ```

5. Now do cheery-pick and then push the master branch again

  ``` bash
    git cherry-pick <commit-hash>
    git push
  ```


  ![Solved screenshot](image.png)
