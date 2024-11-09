# Git Tutorial
## Q2
This question part has been added by main branch. 

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

## How to go to some previous commits back? 
If you want to go to some previous commits back you can use 2 below ways. 
The first way is recommended. 
```bash
git revert -m 1 <commit_id> # use -m 1 for specify parrent commit of merge commits
```
Second way just reset your commit in your local computer and dont reset in others repo. 
```bash
git reset --hard <commit_id>
```

## Git Merge
In all below options you can see your branch's logs with below option. 
```bash
git log --oneline -a --graph
```
You can create a new branch trough below one.
```bash
git branch test
```
And you can see diff of your branch with main one through below one. 
```bash
git diff test..main
git diff main..test
# or also below 
git checkout main
git diff test
```
First suppose the branch that you want to merge it into main branch has not diverge with
main branch. In this option you can do Fast-Forward merge like below. 
```bash
git checkout main
git merge
```
It uses Fast-Forward merging by-default. If you want to dont use that you can do below 
one.(This option is recommended.) 
```bash
git checkout main
git --no-ff merge
```
You can also use rebase way to merge the branches.
```
git checkout test
git rebase main
git switch main
git merge test
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



## Steps to Add Docker Container Key to GitHub
1. **Generate SSH Key in Docker Container**:
   ```bash
   docker exec -it <container_id_or_name> /bin/bash
   apt-get install openssh-client
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```
   Follow the prompts to save the key (e.g., `/root/.ssh/id_rsa`) and optionally set a passphrase.
2. **Copy the Public Key**:
   ```bash
   cat /root/.ssh/id_rsa.pub
   ```
   This command displays the public key. Copy it to your clipboard.
3. **Add SSH Key to GitHub**:
   - Log in to your GitHub account.
   - Go to **Settings** > **SSH and GPG keys** > **New SSH key**.
   - Paste the copied public key and give it a recognizable title (e.g., "Docker Container").
4. **Configure SSH in Docker Container**:
   Create a `config` file in your SSH directory:
   ```bash
   nano /root/.ssh/config
   ```
   Add the following configuration:
   ```config
   Host github.com
       HostName github.com
       User git
       IdentityFile /root/.ssh/id_rsa
   ```
5. **Test SSH Connection**:
   Test the connection to GitHub:
   ```bash
   ssh -T git@github.com
   ```
   You should see a message like "Hi username! You've successfully authenticated, but GitHub does not provide shell access."
### Ensure Simultaneous Access
You now have both your local computer and Docker container configured to access your GitHub repositories. When cloning or interacting with repositories, ensure you’re using SSH URLs:
```bash
git clone git@github.com:username/repo.git
```

## How to add github's IP address to your /etc/hosts file? 
```bash
echo "185.199.108.133 raw.githubusercontent.com" | sudo tee -a /etc/hosts
```








