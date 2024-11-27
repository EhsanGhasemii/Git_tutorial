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

## How to add submodules to your project?
Adding another Git project as a submodule in your existing Git project is a handy way to include external repositories as part of your own project. Here’s a step-by-step guide to help you set it up:

1. **Navigate to your main Git project directory:**
   ```bash
   cd /path/to/your/main/project
   ```

2. **Add the submodule:**
   Replace `URL_OF_SUBMODULE_REPO` with the URL of the repository you want to add as a submodule.
   ```bash
   git submodule add URL_OF_SUBMODULE_REPO path/to/submodule
   ```

3. **Initialize and update the submodule:**
   ```bash
   git submodule update --init --recursive
   ```

4. **Commit the changes:**
   ```bash
   git add .
   git commit -m "Added submodule"
   ```

5. **Push the changes to your remote repository:**
   ```bash
   git push origin main
   ```

**Key Points:**
- The `path/to/submodule` is where you want the submodule to be located within your main project directory.
- The `--recursive` option in the `git submodule update` command ensures that any nested submodules are also initialized and updated.

Now you have another Git project added as a submodule in your main project! If you ever need to update the submodule to a later version, navigate to the submodule directory and use `git pull` to fetch the latest changes:

```bash
cd path/to/submodule
git pull origin main
```

And if you want to remove the submodule, follow these steps:
1. Delete the relevant line from the `.gitmodules` file.
2. Remove the submodule's entry from `.git/config`:
   ```bash
   git config --remove-section submodule.path/to/submodule
   ```

3. Delete the submodule directory from the superproject’s `.git/modules` directory:
   ```bash
   rm -rf .git/modules/path/to/submodule
   ```

4. Remove the submodule directory:
   ```bash
   git rm -r path/to/submodule
   ```

5. Commit the changes:
   ```bash
   git add .
   git commit -m "Removed submodule"
   git push origin main
   ```


## How to clone other branches as main one in to your directory?
When you clone a repository from GitHub, it only clones the default branch (typically `main` or `master`). To see and work with other branches, you need to fetch them after cloning the repository. Here’s how you can do it:

### Steps to Fetch All Branches
1. **Clone the Repository**:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Fetch All Branches**:
   Fetch all branches from the remote repository:
   ```bash
   git fetch --all
   ```

3. **List All Branches**:
   To list all branches, both local and remote:
   ```bash
   git branch -a
   ```

4. **Checkout to a Specific Branch**:
   To switch to a specific branch, use the `checkout` command:
   ```bash
   git checkout <branch-name>
   ```

### Example
If you want to clone the repository and switch to a branch named `develop`, you would do the following:
```bash
git clone <repository-url>
cd <repository-directory>
git fetch --all
git checkout develop
```

### Explanation
- **`git fetch --all`**: This command fetches all branches and tags from the remote repository.
- **`git branch -a`**: Lists all branches, including remote branches.
- **`git checkout <branch-name>`**: Switches to the specified branch.


## How to pull after commiting something? 
The error you're encountering happens when the remote repository contains commits that are not present in your local repository. To resolve this issue, you'll need to integrate the remote changes into your local branch before pushing your changes. Here’s a step-by-step guide to resolve the conflict:

### Step-by-Step Solution

1. **Fetch the Latest Changes from the Remote Repository**:
   ```bash
   git fetch origin
   ```

2. **Merge the Remote Changes into Your Local Branch**:
   ```bash
   git merge origin/main
   ```
   If your main branch is named `main`. If it's `master`, use `git merge origin/master`.

   - If there are conflicts during the merge, Git will prompt you to resolve them manually. Open the conflicting files, resolve the conflicts, and then mark them as resolved:
     ```bash
     git add <file>
     ```

3. **Commit the Merge (If Necessary)**:
   If there were conflicts and you resolved them, you might need to commit the merge:
   ```bash
   git commit -m "Resolved merge conflicts"
   ```

4. **Push Your Changes to the Remote Repository**:
   Now that your local branch is up to date with the remote branch, you can push your changes:
   ```bash
   git push origin main
   ```

### Explanation
- **`git fetch origin`**: This command fetches the latest changes from the remote repository without merging them into your local branch.
- **`git merge origin/main`**: This command merges the fetched changes into your local branch. Replace `main` with your branch name if it’s different.
- **Resolve Conflicts**: If there are conflicts, Git will pause the merge and prompt you to resolve them manually. After resolving the conflicts, you need to add the resolved files and commit the changes.
- **`git push origin main`**: Finally, push your changes to the remote repository.

### Alternative: Rebase
Another approach is to use `git pull --rebase`, which rewrites your local commits on top of the fetched commits:
1. **Pull with Rebase**:
   ```bash
   git pull --rebase origin main
   ```
2. **Resolve Conflicts (If Any)**: If there are conflicts, resolve them as described above.
3. **Push Your Changes**:
   ```bash
   git push origin main
   ```

Using rebase can keep your commit history cleaner by avoiding merge commits.

Give these steps a try, and let me know if you encounter any issues or need further assistance! 😊



## How to figure out diff of your tracken file wiht a specefic commit?
```bash
git diff <commit_hash> -- examplt.txt
```
