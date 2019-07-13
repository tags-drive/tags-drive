# Tags Drive

**Tags Drive** is an open source standalone cloud drive. The main feature of **Tags Drive** is no folders. Instead, every file can have a tag (or tags).

![GitHub release](https://img.shields.io/github/release/tags-drive/core.svg?style=flat-square&label=Backend%20version)
![GitHub release](https://img.shields.io/github/tag-pre/tags-drive/core.svg?style=flat-square&label=Backend%20beta-version)

![GitHub release](https://img.shields.io/github/release/tags-drive/web.svg?style=flat-square&label=Frontend%20version)
![GitHub release](https://img.shields.io/github/tag-pre/tags-drive/web.svg?style=flat-square&label=Frontend%20beta-version)

## Wiki

There's a [Wiki](WIKI.md) for **Tags Drive**.

## Why I should prefer Tags Drive to other cloud drives

For example, you want to save an image of a cat. You can save it into folder `cats` or into folder `cute`. Of course, you may keep 2 equal files, but it would be better to use the tags system. So, you just should to add tags `cat` and `cute` to the photo.

## Installation

### Requirements

- Docker

### Running

1. Pull the latest release from [Docker Hub](https://hub.docker.com/)

    `docker pull kirtis/tags-drive:latest`

1. Prepare folders

    Create a folder `tags-drive` and several sub-folders:

    - `var`
    - `var/data`
    - `ssl` (if you want to use HTTPS)

    CD to `tags-drive` folder.

1. Create an env file and a script to run a docker container

    **Env file** – `tags-drive.env`

    ```bash
    TLS=true
    LOGIN=user
    PSWRD=qwerty
    ENCRYPT=true
    ```

    [List of all env variables](https://github.com/tags-drive/core#environment-variables)

    **Script** – `run.sh`

    ```sh
    #!/bin/bash

    docker run --rm -d \
      --name tags-drive \
      -p 80:80 \
      -v $PWD/var:/app/var \
      -v $PWD/ssl:/app/ssl \
      --env-file $PWD/tags-drive.env \
      kirtis/tags-drive:latest
    ```

1. Generate a self-signed TLS certificate (optional)

    `openssl req -x509 -nodes -newkey rsa:2048 -sha256 -keyout ./ssl/key.key -out ./ssl/cert.cert`

1. Run `run.sh` script

## Infrastructure

There are several repositories:

- [tags-drive/core](https://github.com/tags-drive/core) - contains backend part (written in **Go**)
- [tags-drive/web](https://github.com/tags-drive/web) - contains web part (written in **Vue.js** and **TypeScript**)
- [tags-drive/scripts](https://github.com/tags-drive/scripts) - contains scripts for the deployment
