### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

Nautilus developers are actively working on one of the project repositories, `/usr/src/kodekloudrepos/media`. Recently, they decided to implement some new features in the application, and they want to maintain those new changes in a separate branch. Below are the requirements that have been shared with the DevOps team:

1. On Storage server in Stratos DC create a new branch `xfusioncorp_media` from `master` branch in `/usr/src/kodekloudrepos/media` git repo.
2. Please do not try to make any changes in the code



# solution :-

1. Login to the storage server and then switch to the root user(else u will get the permission error).

2. Switch to the master branch because you need to create a branch from master then , create a branch using the given two ways :-

        - Create and Switch to a New Branch Immediately 
         
                ``` bash 
                        git checkout -b <new_branch_name>
                ```
        
        - Create a New Branch Without Switching to It 

                ``` bash 
                        git branch <new-branch-name>
                ```



