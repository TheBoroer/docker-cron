# Introduction
I quickly whipped this container image together because I needed a container that can just run remote monitoring/alerting bash and python scripts. It has the ability to pull files (and repull/update files when redeploying/restarting the container) from git through the use of environment configurable parameters.

# Building from source
To build this from source you need to clone the public github repo then run docker build:

`git clone https://github.com/TheBoroer/docker-cron .`

`docker build -t docker-cron:latest .`

# Pulling from Docker Hub
`docker pull boro/docker-cronjob`

The docker hub automated build can be found here: https://hub.docker.com/r/boro/docker-cron/

# Basic Usage
Just pull and run this image while mounting your crontab file to `/etc/cron.d/container-cron`.
You can also mount your folder with bash or python (or any other) scripts to `/cron-src/`.

# Available Configuration Options (Environment variables)
- **GIT_NAME** : Set your name for code pushing (required for git to work)
- **GIT_EMAIL** : Set your email for code pushing (required for git to work)
- **GIT_PERSONAL_TOKEN** : Personal access token for your git account (required for HTTPS git access)
- **GIT_REPO** : URL  to the repository containing your source code (without https://). 
  Example: `github.com/username/project`
- **GIT_BRANCH** : Select a specific branch (optional).
- **GIT_REPULL** : If this is set to 1 then every time the container is restarted/redeployed it will pull the latest files from your git repo branch, discarding any local changes. Default: 0

# Automatic Git Pull
It pulls all files from the specified repo/branch to `/cron-src/`. If a `crontab` file is found inside your repo, it will be copied to `/etc/cron.d/container-cron` automatically upon finishing pulling all the files via git.

# Personal Access Token
You can pass the container your personal access token from your git account using the GIT_PERSONAL_TOKEN flag. This token must be setup with the correct permissions in git in order to push and pull code.

Since the access token acts as a password with limited access, the git push/pull uses HTTPS to authenticate. You will need to specify your GIT_USERNAME and GIT_PERSONAL_TOKEN variables to push and pull. You'll need to also have the GIT_EMAIL, GIT_NAME and GIT_REPO common variables defined.

# Example Docker Cloud Stack File
Coming Soon!
