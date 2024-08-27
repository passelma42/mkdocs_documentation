# GIT - the works  

## **Step 1: Initialize a Local Git Repository**  

1. **Open Terminal/Command Prompt**:
   - Use Git Bash, Command Prompt, or PowerShell on Windows.
   - Use Terminal on macOS or Linux.

2. **Navigate to the Folder**:
   ```bash
   cd /path/to/your/local/folder
   ```
   Replace `/path/to/your/local/folder` with the path to your folder.

3. **Initialize the Git Repository**:
   ```bash
   git init
   ```
   This command initializes a new Git repository in your local folder.

## **Step 2: Add Files and Make an Initial Commit**  

1. **Add Files to the Repository**:
   ```bash
   git add .
   ```
   This adds all files in the current directory to the staging area.

2. **Make an Initial Commit**:
   ```bash
   git commit -m "Initial commit"
   ```
   This commits the staged files to the repository with the message "Initial commit."

## **Step 3: Create a New Repository on GitHub**  

1. **Log in to GitHub**:  
   Go to [GitHub](https://github.com) and log in to your account.

2. **Create a New Repository**:
   - Click the "+" icon at the top-right corner and select "New repository."
   - Fill in the repository name and description.
   - Choose whether the repository should be **Public** or **Private**.
   - Do **not** initialize the repository with a README, `.gitignore`, or license.

3. **Create the Repository**:
   - Click "Create repository."

## **Step 4: Link Local Repository to Remote GitHub Repository**  

1. **Copy the Remote Repository URL**:
   - On the new repository page, copy the SSH URL (e.g., `git@github.com:username/repository.git`).

2. **Add the Remote Repository**:
   ```bash
   git remote add origin git@github.com:username/repository.git
   ```
   Replace `git@github.com:username/repository.git` with your copied URL.

3. **Push the Local Repository to GitHub**:
   ```bash
   git push -u origin master
   ```
   This pushes your local commits to GitHub. The `-u` flag sets the upstream tracking for the `master` branch.

## **Step 5: Set Up SSH Access to GitHub**  

1. **Check for Existing SSH Keys**:
   ```bash
   ls -al ~/.ssh
   ```
   Check if you already have SSH key pairs like `id_rsa` and `id_rsa.pub`.

2. **Generate a New SSH Key (if needed)**:
   ```bash
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```
   Replace `"your_email@example.com"` with your GitHub email. Accept the default file location and set a passphrase if desired.

3. **Add SSH Key to the SSH Agent**:
   Start the SSH agent:
   ```bash
   eval "$(ssh-agent -s)"
   ```
   Add your SSH private key:
   ```bash
   ssh-add ~/.ssh/id_rsa
   ```

4. **Add SSH Key to GitHub**:
   - Copy the SSH key to your clipboard:
     ```bash
     cat ~/.ssh/id_rsa.pub
     ```
     Copy the output.
   - Go to GitHub -> Settings -> SSH and GPG keys -> New SSH key.
   - Paste the key, give it a title, and click "Add SSH key."

5. **Modify the `.ssh/config` File**:
   - Open or create the `.ssh/config` file:
     ```bash
     nano ~/.ssh/config
     ```
   - Add the following configuration:
     ```plaintext
     # Configuration for HOST1 access
     Host HOST1
         HostName 000.000.11.30
         User User1
         IdentityFile ~/.ssh/id_rsa_HOST1

     # Configuration for HOST2 access
     Host HOST2
         HostName 000.000.11.11
         User User2
         Port 22
         IdentityFile ~/.ssh/id_rsa_HOST2

     # Configuration for GitHub access (git-HOST3 account)
     Host git-HOST3
         HostName github.com
         User git
         IdentityFile ~/.ssh/id_rsa_git-HOST3
         AddKeysToAgent yes

     # Configuration for GitHub access (git-HOST4 enterprise account)
     Host git-enterprise
         HostName github.com
         User git
         IdentityFile ~/.ssh/id_wsl_git-HOST4
         AddKeysToAgent yes
     ```

6. **Test SSH Connection**:
   ```bash
   ssh -T git@git-HOST3
   ```
   This command tests if you can authenticate with GitHub using the configured key. You should see a message like `Hi username! You've successfully authenticated...`.

## **Step 6: Configure Git Settings for the Folder**  

1. **Set Your Username and Email**:
   ```bash
   git config user.name "Your Name"
   git config user.email "your_email@example.com"
   ```
   Replace `"Your Name"` and `"your_email@example.com"` with your actual name and email.

2. **Set Default Push Behavior**:
   ```bash
   git config push.default simple
   ```
   This ensures that `git push` pushes only the current branch.

3. **Verify Your Configuration**:
   ```bash
   git config --list
   ```
   This command lists all your Git configurations to verify they are set correctly.

## **Step 7: Using Git in Your Project**  

1. **Check Status**:
   ```bash
   git status
   ```

2. **Stage Changes**:
   ```bash
   git add .
   ```

3. **Commit Changes**:
   ```bash
   git commit -m "Your commit message"
   ```

4. **Push Changes**:
   ```bash
   git push
   ```

This complete guide will help you set up a local Git repository, connect it to a GitHub repository using SSH, and configure your SSH and Git settings properly.