# Introduction
I quickly whipped this container image together because I needed a container that can just run remote monitoring/alerting bash and python scripts. It has the ability to pull files (and repull/update files when redeploying/restarting the container) from git through the use of environment configurable parameters.

# Building from source
To build this from source you need to clone the public github repo then run docker build:
```git clone https://github.com/TheBoroer/docker-cronjob .```
```docker build -t docker-cronjob:latest .```

# Pulling from Docker Hub
```docker pull boro/docker-cronjob```
The docker hub automated build can be found here: __________________________

# Available Configuration Options (Environment variables)
- **GIT_REPO** : URL  to the repository containing your source code (without https://). 
  Example: `github.com/username/project`
- **GIT_BRANCH** : Select a specific branch (optional).
- **GIT_EMAIL** : Set your email for code pushing (required for git to work)
- **GIT_NAME** : Set your name for code pushing (required for git to work)
- **GIT_PERSONAL_TOKEN** : Personal access token for your git account (required for HTTPS git access)
- **GIT_REPULL** : If this is set to 1 then every time the container is restarted/redeployed it will pull the latest files from your git repo branch, discarding any local changes. Default: 0

# Example Usage
