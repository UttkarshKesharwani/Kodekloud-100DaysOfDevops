### Do follow for more such content
### Linkdin URL :- https://www.linkedin.com/in/uttkarsh-kesharwani-a321712b1/


# Problem Statement :-

The Nautilus application development team was working on a git repository `/opt/media.git` which is cloned under `/usr/src/kodekloudrepos` directory present on Storage server in Stratos DC. The team want to setup a hook on this repository, please find below more details:

1. Merge the `feature` branch into the `master` branch, but before pushing your changes complete below point.
2. Create a `post-update` hook in this git repository so that whenever any changes are pushed to the mas`ter branch, it creates a release tag with name `release-2023-06-15`, where `2023-06-15` is supposed to be the current date. For example if today is `20th June, 2023` then the release tag must be `release-2023-06-20`. Make sure you test the hook at least once and create a release tag for today's release.
3. Finally remember to `push` your changes.

Note: Perform this task using the `natasha` user, and ensure the repository or existing directory permissions are not altered.




# Thing to know :- 

1. What is git hooks ?
  
  - Git Hooks are scripts that run automatically when certain Git events(like push,commit,pull,merge etc) happens.Think of them like: “Triggers inside Git that run before or after actions like commit, push, merge.”
  
  - Sample examples :- 
      When you do: `git commit -m "added login"` Before the commit is saved, Git can run a script file. That script is called pre-commit hook . Simlarly for the push , pull merge event , use can explore the things at `.git/hooks` directory

  ``` bash

      [natasha@ststor01 media]$ ls -a
      .  ..  .git  feature.txt  info.txt

      cd .git/

      [natasha@ststor01 .git]$ ls -a
      .   COMMIT_EDITMSG  branches  description  index  logs     refs
      ..  HEAD            config    hooks        info   objects

      cd hooks/

      [natasha@ststor01 hooks]$ ls -a
      .                          pre-applypatch.sample    prepare-commit-msg.sample
      ..                         pre-commit.sample        push-to-checkout.sample
      applypatch-msg.sample      pre-merge-commit.sample  sendemail-validate.sample
      commit-msg.sample          pre-push.sample          update.sample
      fsmonitor-watchman.sample  pre-rebase.sample
      post-update.sample         pre-receive.sample

  ```

  you can see there are multiple git hooks are present , you can see them and explore by yourself for better understanding 


# Usecases of git hooks

- **Tagging**: Automatic version tagging
- **Code Quality**: Run linters, formatters
- **Notifications**: Send alerts on repository changes
- **Testing**: Execute test suites before commits
- **Deployment**: Automatic deployment on push





# Solution :-

1. Learn/Undestand , what is git hooks ? , go to the #Things to know section

2. Login user on correct server

3. Make the post-update hook
  
  - move to the git repo 
    `cd /opt/beta.git`

  - check the content inside the current working directory
    `ls -a`

    you will see here `hooks` directory

  - move to the hooks directory 
    `cd hooks/` (In this place you will put all the hooks file , which get triggered when any action is occured)

  - make the `post-update` file and then give the execute permission 
    ``` bash
      cp post-update.sample post-update && chmod +x post-update
    ```
  
  - open the post-update file and put the content below , inside it 
    ``` text 
      day=$(date +"%Y-%m-%d")
      TAG="release-$day"
      git tag "$TAG" refs/heads/master
    ```

4. Move to the clone repo directory and then merge the feature branch into main branch

  ``` bash

      cd /usr/src/kodekloudrepos/media
      git branch
      git checkout master
      git merge feature

  ```

5. Now , push the master branch

  ```bash 
    git push
  ```

6. Verify the tag

    ```sh
      git fetch --tags
      git tag
    ```



