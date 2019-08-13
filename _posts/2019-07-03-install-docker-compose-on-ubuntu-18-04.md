---
layout: post
title:  "Install docker-compose on ubuntu server 18.04"
date:   2019-07-03 19:10:44 -0300
categories: linux ubuntu services docker compose
---
## Requirements:
* Docker is already installed on system.

### 1. Download the Docker Compose binary into the `/usr/local/bin` directory

```sh
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### 2. Once the download is complete, apply executable permissions to the Compose binary:

```sh
sudo chmod +x /usr/local/bin/docker-compose
```

### 3. Verify installation:
```sh
docker-compose --version
```

```sh
Output

docker-compose version 1.23.1, build b02f1306
```
