Git Deploys with Dropbox and Wordpress
======================================

Setting up git to automagically mirror to dropbox as a backup, and deploy to a remote server when you are ready to push. This can work with any website, but I'm using Wordpress as an example.

Prerequisites
--------------
1. Download MAMP
2. Download wordress
3. Create MAMP database
4. Setup local database info for MAMP in wp-config.php
5. Install git (I use homebrew to install)
6. Install Dropbox

Setup
--------------
1. Setup git repo in the root of your local wordpress install.
    cd [wordpress root directory]
    git init
2. Add wordpress files to .gitignore file in root directory. These will be the files we'll keep from deploying later.
3. Make a repo folder in Dropbox to hold your multitude of kick ass git repos. Then create your repo and initialize it.
    cd ~/Dropbox
    mkdir gitRepos
    cd gitRepos
    mkdir repoName.git
    cd repoName.git
    git --bare init
4. Add git remote for Dropbox, then push your branch there. In my case, I'm using the branch master, which is the default. This remote target will be our server we keep our repo synced to.
    cd [wordpress root directory]
    git remote add
    git add remote dropbox file:///$HOME/Dropbox/gitRepos/repoName.git
    git push dropbox master
