

## **What is a “version control system”?** 

Version control systems are a category of software tools that helps in recording changes made to files by keeping a track of modifications done in the code.

## **Why Version Control system is so Important?**
Basically Version control system keeps track on changes made on a particular software and take a snapshot of every modification. Let’s suppose if a team of developer add some new functionalities in an application and the updated version is not working properly so as the version control system keeps track of our work so with the help of version control system we can omit the new changes and continue with the previous version.

## **Benefits of the version control system:**

- Enhances the project development speed by providing efficient collaboration,
- Leverages the productivity, expedites product delivery, and skills of the employees through better communication and assistance,
- Reduce possibilities of errors and conflicts meanwhile project development through traceability to every small change,
- Employees or contributors of the project can contribute from anywhere irrespective of the different geographical locations through this **VCS,**
- For each different contributor to the project, a different working copy is maintained and not merged to the main file unless the working copy is validated. 
- Helps in recovery in case of any disaster or contingent situation,
- Informs us about Who, What, When, Why changes have been made.

## **Types Of VC**
## Local Version Control (LVC)![[Pasted image 20241214152808.png]]

## Central Version Control (CVC)
![[Pasted image 20241214152852.png]]

## Distributed Version Control (DVC)

![[Pasted image 20241214152914.png]]



### **. Introduction to Git**

#### **What is Git?**

- Git is a **distributed version control system** that allows multiple developers to collaborate on a project by tracking changes to the codebase.
- **Distributed** means each contributor has a full copy of the repository, including the project’s entire history.

#### **Install Git**

[Git - Downloads](https://git-scm.com/downloads) 

#### **Setup Git
```
# Set global username and email (required for commit tracking)
git config --global user.name "yourname"
git config --global user.email "yourEmail"

# Verify configuration
git config --global --list

```

#### **Initializing a Git Repository
```
mkdir my_project          # Create a new folder for the project
cd my_project             # Navigate into the project folder
git init                  # Initialize a Git repository

```

- `git init` creates a hidden `.git` folder where Git tracks changes.

#### **Check Repository Status
```
git status
```


----


#### **Setting your text editor
By default, git uses systems default editor. This can be configured by:
```
git config --global core.editor vim
```


#### **Track everything with unique id

```
echo "Hello, Git" | git hash-object --stdin
```

```
echo "Hello, Git" | shasum
```

```
echo -e "blob 11\0Hello, Git" | shasum
```

![[Pasted image 20241218004727.png]]

**Remember!**  

#### **Each file is:

- **_Untracked_: (Git does not care about it but will keep alerting you)**

- **_Tracked_:**  

    - **Unmodified (Either never changed since tracked, or commited and never changed afterwards)**

    - **Modified (Either doesn't have a snapshot or been changed since last commit)**

    - **Staged (Had some changes and ready to be committed)**
    ![[Pasted image 20241218015550.png]]
   
#### **Commands

```
git diff # difference between staged and WT
```

```
git diff --staged  #or --cached To show differencce between staged and Commiited
```


```
  git diff <begincommitrefs>..<endcommitrefs> `` # # Show changes between Commits (Compare commits) Refs is the SHA of the commit 
```

```
git ls-files #list all files on staging area
```

```
find .git/objects/ -type f # to get files on .git repo
```

```
git cat-file -p, -s, -t  # for learning about blob and tree
```

```
git commit -m "Commit message" # commit files to git repo
```

```
git commit -a -m "<msg>" #skipping staging area
```


**A branch in Git is simply a lightweight movable pointer to one of these commits.** 
**master is the default name of the branch**

```
git show
```

#### **Undoing things

```
git rm --cached <filename> # untracked tracked files
```

```
git restore  <filenmame> # discard unstaged modification
```

```
git restore --staged <filenmame> # unstaged staged file
```

```
git commit --amend # edit last commit
```

```
git reset --hard HEAD~2  # moving head two steps back
```

```
git reflog # show changes made
```

```
git reset --hard HEAD@{} #fast fowroward
```

```
git branch testing # create new branch without swithing to it
```

```
git switch testing # switch to testing branch
```

```
git switch master && git merge testing # merge testing to master branch
```

```
git remote && git remote -v
```
.
