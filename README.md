Git Deploys with Dropbox and Wordpress
======================================

Setting up git to mirror to dropbox as a backup, and deploy to a remote server when you are ready to push.

Prerequisites
--------------
1. Download MAMP
2. Download wordress
3. Create MAMP database
4. Setup local database info for MAMP in wp-config.php
5. Install git (I use homebrew to install)

Setup
--------------
1. Setup git repo:
  cd [wordpress root directory]
  git init
2. Add wordpress files to .gitignore
