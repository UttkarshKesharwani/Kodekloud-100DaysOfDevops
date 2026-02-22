
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus application development team has been working on a project repository `/opt/media.git`. This repo is cloned at `/usr/src/kodekloudrepos` on storage server in Stratos DC. They recently shared the following requirements with DevOps team:

Create a new branch xfusion in `/usr/src/kodekloudrepos/media` repo from master and copy the `/tmp/index.html` file (present on storage server itself) into the repo. Further, add/commit this file in the new branch and merge back that branch into master branch. Finally, push the changes to the origin for both of the branches.

# Solution :-

1, Login into Storage server(do it by yourself)

2. Move into repository and then switch to the root user:

    ```sh
    sudo su -
    cd /usr/src/kodekloudrepos/media
    ```

3. Create a new branch from master (ensure current branch is master branch , using ` git branch`)

    ```sh
      git checkout -b nautilus
    ```
4. Copy files

    ```sh
    cp /tmp/index.html /usr/src/kodekloudrepos/media
    ```
5. Commit changes

    ```sh
    git add .
    git commit -m "added index.html"
    ```

6. Switch to master branch

    ```sh
    git switch master
    ```
7. Finally Merge `nautilus` the branch and then push chnages

    ```sh
    git merge nautilus
    git push
    ```

