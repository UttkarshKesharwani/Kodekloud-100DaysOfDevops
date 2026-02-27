### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus application development team was working on a git repository `/usr/src/kodekloudrepos/media` present on Storage server in Stratos DC. This was just a test repository and one of the developers just pushed a couple of changes for testing, but now they want to clean this repository along with the commit history/work tree, so they want to point back the `HEAD` and the branch itself to a commit with message `add data.txt file`. Find below more details:

1. In `/usr/src/kodekloudrepos/media` git repository, reset the git commit history so that there are only two commits in the commit history i.e initial commit and `add data.txt file`.
2. Also make sure to push your changes.


# Solution :- 

1. Login to the server and become root user(do it by yourself)

2. Move to the correct directory

  ``` bash 
      cd /usr/src/kodekloudrepos/media
  ```

3. Check the current branch and the log all the commit 

  ``` bash 
      git branch 
      git log --oneline --all --graph
  ```

  you will see:-

  ``` text   
      [root@ststor01 media]# git branch 
      * master
      [root@ststor01 media]# git log --oneline --all --graph
      * d2beb47 (HEAD -> master, origin/master) Test Commit10
      * 3732f8a Test Commit9
      * 10c0101 Test Commit8
      * 3c2666d Test Commit7
      * 5dc93ca Test Commit6
      * 0a90631 Test Commit5
      * 527c3d2 Test Commit4
      * 3de09e8 Test Commit3
      * eddf805 Test Commit2
      * 254e4ab Test Commit1
      * f7d80aa add data.txt file
      * 0b42efe initial commit
  ```

4. Do hard reset and then push the changes 

  ``` bash 
      git reset --hard f7d80aa
      git push --force 
  ```

# Things to know 

1. Diff bw reset v/s revet
  - The main difference is that git reset modifies (rewrites) the project history by moving the branch pointer to a previous commit, while git revert undoes changes by creating a new commit that reverses the specified commit's effects, thereby preserving the original history. 


