
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-
The Nautilus application development team was working on a git repository `/usr/src/kodekloudrepos/cluster` present on Storage server in Stratos DC. One of the developers stashed some in-progress changes in this repository, but now they want to restore some of the stashed changes. Find below more details to accomplish this task:

- Look for the stashed changes under `/usr/src/kodekloudrepos/cluster` git repository, and restore the stash with `stash@{1}` identifier. Further, commit and push your changes to the origin.





# Solution  :- 

1. Login to the server and switch to the root user and then navigate to the directory

2. List the stash

  ``` bash 
    git stash list
  ```

  You will see like :- 
  ``` text
    stash@{0}: WIP on master: 7fe985d initial commit
    stash@{1}: WIP on master: 7fe985d initial commit
    Restart stash files
  ```

3. Apply the stash

  ``` bash
    git stash apply stash@{1}
  ```

4. Push changes

  ``` bash
    git add .
    git commit -m "Restored stash files"
    git push
  ```