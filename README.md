# Tags Drive

**Tags Drive** is an open source standalone cloud drive. The main feature of **Tags Drive** is no folders. Instead, every file has a tag (or tags).

## Wiki

There's a [wiki document](WIKI.md).

## Why I should prefer Tags Drive to other cloud drives

For example, you want to save an image of a cat. You can save it into folder `cats` or into folder `cute`. Of course, you may keeps 2 equal files, but it would be better to use tags system. So, you just should to add tags `cat` and `cute` to the photo.

## Installing

**Requirements:**

- Docker

Run `docker pull kirtis/tags-drive`. Create folder `tags-drive` and several sub-folders: `configs`, `data`, `ssl` (you you want to use HTTPS). CD to this folder.

Create `run.sh` to run docker container. Example:

```sh
#!bin/bash

docker run --rm -d \
  --name tags-drive \
  -p 80:80 \
  -v $PWD/configs:/app/configs \
  -v $PWD/data:/app/data \
  -v $PWD/ssl:/app/ssl \
  --env-file $PWD/tags-drive.env \
  kirtis/tags-drive:latest
```

Example of `tags-drive.env`:

```bash
PORT=80
TLS=true
LOGIN=user
PSWRD=qwerty
ENCRYPT=false
DBG=false
```

**Environment variables:**

[List of env variables](https://github.com/tags-drive/core#environment-variables)

## Infrastructure

There are several repositories:

- [tags-drive/core](https://github.com/tags-drive/core) - contains backend part (written in **Go**)
- [tags-drive/web](https://github.com/tags-drive/web) - contains web part (written in **Vue.js**)
- [tags-drive/scripts](https://github.com/tags-drive/scripts) - contains scripts for deployment