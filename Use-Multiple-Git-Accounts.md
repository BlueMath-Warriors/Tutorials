# Use Multiple Git Accounts on single PC

## Generate new SSH key 

In order to connect to this account's repositories we need to generate a separate SSH key. The key name would be as follows: `id_rsa_account_name`

key-gen command

    ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa_arith

Copy key Command

    cat ~/.ssh/id_rsa_arith.pub

Add this copied key to the github account settings.

## Generate new SSH config

SSH configuration files provide a means to specify which SSH key should be used for a specific repository. To implement this, an individual SSH config file needs to be set up for this SSH key.

Create new file

    touch ~/.ssh/config-github-account-name

Edit File

    nano ~/.ssh/config-github-account-name

Place the following config

    # ~/.ssh/config-arith
    Host github.com
        HostName github.com
        Port 22
        User git
        IdentityFile ~/.ssh/id_rsa_arith

## Setup the Repo Locally

We will setup a empty repository locally and updates it's remote origin to a particular repo we want to,

Create Folder

    mkdir repo-name

Switch to repo-name

    cd repo-name

Initiate the git repo: this will make this repo a local empty repo

    git init

## Add the local git configs

Now, we will configure this local empty repo to use the particular user and ssh key.

Add the user name

    git config user.name "github-username"


Add the user email

    git config user.email "github-email@host"

Add the remote url

    git remote add origin git@github.com:github-ssh-url-for-repo

Add the ssh config to be used for this repo

    git config core.sshCommand "ssh -F ~/.ssh/config-arith"

Use the following command to check that the local configurations are correct.

    git config --list --show-origin

Now, fetch the remote branches using the following

    git fetch -a

