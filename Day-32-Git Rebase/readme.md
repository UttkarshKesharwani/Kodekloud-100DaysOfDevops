
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus application development team has been working on a project repository `/opt/blog.git`. This repo is cloned at `/usr/src/kodekloudrepos` on storage server in Stratos DC. They recently shared the following requirements with DevOps team:

- One of the developers is working on `feature` branch and their work is still in progress, however there are some changes which have been pushed into the `master` branch, the developer now wants to `rebase` the `feature` branch with the `master` branch without loosing any data from the `feature` branch, also they don't want to add any `merge commit` by simply merging the `master` branch into the `feature` branch. Accomplish this task as per requirements mentioned.
- Also remember to push your changes once done.

# Solution :- 

1. Login to the correct server and switch to the root user (do it by yourself)

2. Navigate to the correct directory 

    ``` sh
      cd /usr/src/kodekloudrepos/blog
    ```

3. Check the status of your branch , ensure you should be at `feature` branch

    ` git status`

4. Rebase the branch

  ```sh
    git rebase main
  ```

5. Push the local working directory 
  
  ```sh
    git push --force --set-upstream origin feature
  ```

