# Git commands
Cheatsheet : https://education.github.com/git-cheat-sheet-education.pdf
Reference : https://git-scm.com/docs
#### To see all the files in the dir
```ls -a```

#### To see no of files in the dir
 ```ls -l```
 #### To see no of files and files and its permissions
 ```ls -la```

#### Configuring git 
``` git config --global user.name = "username" ```
``` git config --global user.email = "emailId" ```
``` git config --global pass.email = "password" ```  Not done for this


#### Initialize a git repository
``` git init ```

#### To displays the state of the working directory and the staging area
``` git status ```

#### To check the branch name
``` git branch ```

#### To rename the current branch 
```git branch -M <branch_name> ```

#### To stage a file 
``` git add <file name> ```

#### Commit staged files or commit a changes
``` git commit -m "<Message about the commit>" ```


#### To see all the changes or logs
 ``` git log  ```
- To see all the logs
``` git log -a ```
- To see commits in one line
``` git log --oneline ```
- To see n number of commits or limits the commits
``` git log -n <number>```

---

## Configuring SSH 

#### Check for Existing SSH Keys
``` ls -al ~/.ssh  ```

#### Generate a New SSH Key
``` ssh-keygen -t ed25519 -C "your_email@example.com" ```

#### Add the SSH Key to the SSH Agent 
Start ssh agent
``` eval "$(ssh-agent -s)" ```

add your key
``` ssh-add ~/.ssh/id_ed25519 ```
#### Add SSH Key to GitHub
Copy your public SSH key:
 
``` cat ~/.ssh/id_ed25519.pub ```


#### Test the connection
``` ssh -T git@github.com ```

ssh-agent -> github.com
github.com (challenge message)-> ssh-client 
ssh-client (decrypts)-> challenge message 
if success -> authenticated ;
####

---


#### Difference between two commits
``` git diff <commit_1 id>..<commit_2 id> ```

#### Moving head one commit back -  removes all the changes and the HEAD permanently
``` git reset --hard HEAD~1 ```
#### Moving head 2 commit back -  removes all the changes and the HEAD permanently
``` git reset --hard HEAD~2 ```

#### Moving head one commit back - removes the commit and stage all the changes of the HEAD
``` git reset --soft HEAD~1 ```

#### Moving head 2 commit back - removes the commit and stage all the changes of the HEAD
``` git reset --soft HEAD~2 ```

#### Unstage a file or folder
``` git reset <file/foldername> ```

#### Remove from stage area
``` git rm --cached <filename> ```

#### Checkout or visit a commit 
* ``` git checkout ```
- ``` git checkout <file name> ```

#### To remove all the untracked files
``` git clean -f ```

#### Show all available branch
```git branch ```

#### Create a new Branch 
``` git branch <branch-name>```

#### To delete a branch
You need to switch to some other branch before deleting
``` git branch -d <branch-name>```
``` ```

#### Merging a branch to main/any branch
``` git merge <branch-name> ```

#### Rebase feature to main
``` git rebase featutre ```

