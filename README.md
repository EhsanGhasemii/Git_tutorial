# Git Tutorial

## How to push some file on Git
```bash
git add -A
git commit -m "your commit"
git push
```

## How you can see your commits? 
```bash
git log
git log -5
git log --grep="part of commit message"
git lot --author="your name"
```

## Transfer to a specefic commit
```bash
git checkout <hash_format_of_your_log>
```

## Transfer to master commit
```bash
git checkout master
git checkout main
```

## How to ignore some files to push on Git? 
First you nedd create a .gitignore file in main directory
```bash
touch .gitignore
vim .gitignore
```
Then write your data path that you want to ignore. 
```bash
/data0/
/main/data1/
```
Then push your .gitignore file to the main directory
```
git add .gitignore
git commit -m "Add .gitignore file"
git push
```

## How to pull the latest changes from the remote repository?
First you should fetch the latest changes from the remote repository. 
```bash
git fetch origin
```
Then you should switch to your brach that you want to pull on. 
```bash
git checkout <branch_name>
```
Then you can merge the latest changes from the remote branch into your branch like below: 
```bash
git merge origin/<branch_name>
```
