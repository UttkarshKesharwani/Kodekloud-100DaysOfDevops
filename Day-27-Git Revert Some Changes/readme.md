
### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-
The Nautilus application development team was working on a git repository `/usr/src/kodekloudrepos/beta` present on Storage server in Stratos DC. However, they reported an issue with the recent commits being pushed to this repo. They have asked the DevOps team to revert repo HEAD to last commit. Below are more details about the task:
1. In `/usr/src/kodekloudrepos/beta` git repository, revert the latest commit ( HEAD ) to the previous commit (JFYI the previous commit hash should be with initial commit message ).
2. Use `revert beta` message (please use all small letters for commit message) for the new revert commit.


# Solution :- 

1. Login to the storage server and then switch to the root user.

2. Naviagte to the correct directory

    ``` bash
      cd /usr/src/kodekloudrepos/beta 
    ```

3. Revert latest commit with custom message

    ``` bash
        git revert HEAD -n
        git commit -m "revert beta"
    ```

    `-n` = make revert but don’t commit yet

4. Push the commit  

    ``` bash
        git push
    ```

# important :-

- you can see all the commit in graph form(visuals) :- `git log --oneline --all --graph`