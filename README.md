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



## How to create SSH in your local computer and connect to github or gitlab?
1. **Check for Existing SSH Keys**:
   Open a terminal and run:
   ```sh
   ls -al ~/.ssh
   ```
   Look for files named `id_rsa` and `id_rsa.pub` or similar. If these files exist, you have an SSH key pair.

2. **Generate a New SSH Key Pair (If Needed)**:
   If you don't have an existing SSH key pair, generate one:
   ```sh
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```
   Follow the prompts and save the key in the default location (`~/.ssh/id_rsa`).

3. **Add Your SSH Key to the SSH Agent**:
   Start the SSH agent and add your SSH key:
   ```sh
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_rsa
   ```

4. **Add Your SSH Key to GitHub**:
   Copy the contents of your public key to the clipboard:
   ```sh
   cat ~/.ssh/id_rsa.pub
   ```
   Then, log in to GitHub, go to **Settings > SSH and GPG keys**, and add a new SSH key with the copied content.

5. **Verify SSH Connection**:
   Test the SSH connection to ensure everything is configured correctly:
   ```sh
   ssh -T git@github.com
   ```
   You should see a success message like:
   ```sh
   Hi username! You've successfully authenticated, but GitHub does not provide shell access.
   ```

6. **Update Remote URL (If Necessary)**:
   If you still encounter issues, you can try using the HTTPS URL instead of SSH:
   ```sh
   git remote set-url origin https://github.com/username/repository.git
   ```



