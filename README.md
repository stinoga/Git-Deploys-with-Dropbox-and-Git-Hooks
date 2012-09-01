Git Deploys with Dropbox and Wordpress
======================================

Setting up git to automagically mirror to dropbox as a backup, and deploy to a remote server when you are ready to push. This can work with any website, but I'm using Wordpress as an example. In the same vein, the remotes are named dropbox and live for simplicity's sake, but you can name them whatever tickles your fancy.

Prerequisites
--------------
1. Download MAMP
2. Download wordress
3. Create MAMP database
4. Setup local database info for MAMP in wp-config.php
5. Install git (I use homebrew to install)
6. Install Dropbox

Setup Dropbox Sync
--------------
1. Setup git repo in the root of your local wordpress install.
```
cd [wordpress root directory]
git init
```
2. Add wordpress files to .gitignore file in root directory. These will be the files we'll keep from deploying later.
3. Make a repo folder in Dropbox to hold your multitude of kick ass git repos. Then create your repo and initialize it.
```
cd ~/Dropbox
mkdir gitRepos
cd gitRepos
mkdir repoName.git
cd repoName.git
git init --bare
```
4. Add git remote for Dropbox, then push your branch there. In my case, I'm using the branch master, which is the default. This remote target will be our server we keep our repo synced to. You can read my full documentation on cloning and then pulling from this remote [here](https://gist.github.com/3340157).
```
cd [wordpress root directory]
git remote add
git add remote dropbox file:///$HOME/Dropbox/gitRepos/repoName.git
git push dropbox master
```
5. Add your post-commit file into the hooks folder in your repo. This will push a mirrored version of all committed files to your remote repo after they are commited, keeping you backed up in Dropbox.
```
[wordpress root directory]/.git/hooks
```

Setup Git Deployment
--------------
1. SSH into your server, and create a remote repo.
```
mkdir repoName.git
cd repoName.git
git init --bare
```
2. Add git remote for live server. You will need to replace the user and host vars below with your site info.
```
cd [wordpress root directory]
git remote add live ssh://[user]@[host]/~/mysite.git
```
