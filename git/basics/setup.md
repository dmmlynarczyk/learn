# Setup

## Installation

### Void

1. To download via CLI on Void Linux, run:
    - ```
       sudo xbps-install -S
       sudo xbps-install git
      ```
2. To verify installation run `git --version`

### Debian

1. To download via CLI on Debian 13, run:
    - `sudo apt install git`
2. To verify installation run `git --version`

### Windows

1. Ensure `winget` is installed on your Windows machine.
   1. I typically use the [App Installer](https://apps.microsoft.com/detail/9nblggh4nns1) to ensure I have the proper package.
2. Run the command `winget install --id Git.Git -e --source winget`
3. To verify installation run `git --version`

## Initial User Setup

Configuring user information used across all local repositories.

`git config --global user.email "email@ddress"`  
*Set an email address that will be associated with each history maker*

`git config --global user.name "firstname lastname"`  
*Set a name that is identifiable for credit when reviewing version history*

`git config --global color.ui auto`  
*Set automatic command line coloring for git for easy reviewing.*  

## SSH

### Linux

1. **Generate a new SSH key:** `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`  
2. **Start the ssh-agent:** `eval "$(ssh-agent -s)"`  
3. **Add private key to ssh-agent:** `ssh-add ~/.ssh/<your_key_name>`  
4. **Copy your public key to add to GitHub profile:** `cat <your_key_name>`  
    - *Copy the public key and paste it into the SSH key section in your GitHub profile settings.*  
5. **Test your SSH key connection:** `ssh -T git@github.com`  
6. **To change your SSH key passphrase:** `ssh-keygen -p -f ~/.ssh/<your_key_name>`  

### Windows

1. **Generate a new SSH key:** `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`  
2. In PowerShell run the following as Administrator:  
   1. **Change ssh-agent startup type:** `Get-Service ssh-agent | Set-Service -StartupType Automatic`  
   2. **Start the service:** `Start-Service ssh-agent`  
   3. **Ensure Status is Running:** `Get-Service ssh-agent`  
   4. **Add your key path:** `ssh-add <complete-key-path-here>`  
3. **Copy your public key to add to GitHub profile:** `cat <your_key_name>`
    - Copy the public key and paste it into the SSH key section in your GitHub profile settings.
4. **Test your connection:** `ssh -T git@github.com`

## INIT

Configuring user information, initializing, and cloning repositories.

`git init`  
*Initialize an existing directory as a git repository*

`git clone <URL>`  
*Retrieve an entire repository from a hosted location via URL.*
