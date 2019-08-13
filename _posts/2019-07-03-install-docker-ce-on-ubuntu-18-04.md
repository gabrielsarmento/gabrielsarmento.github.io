---
layout: post
title:  "Install docker-ce on ubuntu server 18.04"
date:   2019-07-03 19:10:44 -0300
categories: linux ubuntu services docker compose
---


### Step 1 - Enabling Docker repository

#### 1. Update packages list and install dependencies

```sh
sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

#### 2. Import the repository’s GPG

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

#### 3. Add Docker APT repository
```sh
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

### Step 2 - Install Docker CE

#### 1. Update apt repository list and install last version of docker

```sh
sudo apt update
sudo apt install docker-ce
```

#### 2. To install a specific version 
``` sh
apt list -a docker-ce
```

```sh
Output 

docker-ce/bionic 5:18.09.7~3-0~ubuntu-bionic amd64
docker-ce/bionic 5:18.09.6~3-0~ubuntu-bionic amd64
docker-ce/bionic 5:18.09.5~3-0~ubuntu-bionic amd64
```

```sh
sudo apt install docker-ce=5:18.09.6~3-0~ubuntu-bionic
```
#### Optinal - Prevent the Docker package from being automatically updated

```sh
sudo apt-mark hold docker-ce
```

### Step 3 - Post Install

#### 1. Executing docker without `sudo`

```sh
sudo usermod -aG docker $USER
```