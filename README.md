Git Deploys with Dropbox and Git Hooks
======================================

Setting up git to automagically mirror to dropbox as a backup, and deploy to a remote server when you are ready to push. The remotes are named dropbox and live for simplicity's sake, but you can name them whatever tickles your fancy.

Prerequisites
--------------
1. Install git (I use homebrew to install)
2. Install Dropbox
3. Setup SSH access on your site

Setup Dropbox Sync
--------------
1. Setup git repo in the root of your local project.

        cd [project root directory]
        git init

2. Add any files you want to ignore to the .gitignore file in root directory. These will be the files we'll keep from deploying later. You'll want to do an inventory of any files you have locally and don't want to go live.
3. Make a repo folder in Dropbox to hold your multitude of kick ass git repos. Then create your repo and initialize it.

        cd ~/Dropbox
        mkdir gitRepos
        cd gitRepos
        git init --bare repoName.git

4. Add git remote for Dropbox, then push your branch there. In my case, I'm using the branch master, which is the default. This remote target will be our server we keep our repo synced to. You can read my full documentation on cloning and then pulling from this remote [here](https://gist.github.com/3340157).

        cd [project root directory]
        git remote add dropbox ~/Dropbox/gitRepos/repoName.git
        git push dropbox master

5. Add your post-commit file into the hooks folder in your repo. This will push a mirrored version of all committed files to your remote repo after they are commited, keeping you backed up in Dropbox.

        [project root directory]/.git/hooks


Setup Git Deployment
--------------
1. SSH into your server, and create a remote repo. I am creating it in the root directory for this example.

        cd ~
        mkdir repoName.git
        cd repoName.git
        git init --bare

2. While still in your repo folder on the server, create a post-receive file and add in the content from this repo. You'll want to update the FOLDER variable to the directory you are pushing to. I'm using vi to do this, but you can use whatever you like. You may also need to set the correct permissions on this file so we can access it. Use chmod for this.

        vi hooks/post-receive
        chmod 775 hooks/post-receive

3. Clone your newly create repo into the folder that houses your site. Change my wwwRoot var below to the path to that folder.

        cd ~
        git clone repoName.git [wwwRoot]
        exit

4. Add git remote for live server. You will need to replace the user and host vars below with your site info.

        cd [project root directory]
        git remote add live ssh://[user]@[host]/~/mysite.git

5. Push to your site!

        git push live master


Notes
-----

* Once you run your first git push of your branch to either the dropbox or live remotes, you don't HAVE to specify a branch, aka "git push live." This is because git will push all changes on the local branches that have matching remote branches at your target remote.
