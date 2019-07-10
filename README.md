# Tags Drive

**Tags Drive** is an open source standalone cloud drive. The main feature of **Tags Drive** is no folders. Instead, every file can have a tag (or tags).

## Version

The latest version of [backend](https://github.com/tags-drive/core) ![GitHub release](https://img.shields.io/github/release/tags-drive/core.svg)

The latest version of [frontend](https://github.com/tags-drive/web) ![GitHub release](https://img.shields.io/github/release/tags-drive/web.svg)

## Wiki

There's a [Wiki](WIKI.md) for **Tags Drive**.

## Why I should prefer Tags Drive to other cloud drives

For example, you want to save an image of a cat. You can save it into folder `cats` or into folder `cute`. Of course, you may keep 2 equal files, but it would be better to use the tags system. So, you just should to add tags `cat` and `cute` to the photo.

## Installing

**Requirements:**

- Docker

**Setup:**

Run `docker pull kirtis/tags-drive:latest`. Create folder `tags-drive` and several sub-folders: `var`, `var/data`, `ssl` (if you want to use HTTPS). CD to this folder.

Create `run.sh` to run a docker container. Example:

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

Example of `tags-drive.env`:

```bash
TLS=true
LOGIN=user
PSWRD=qwerty
ENCRYPT=true
```

**Environment variables:**

[List of all env variables](https://github.com/tags-drive/core#environment-variables)

## Infrastructure

There are several repositories:

- [tags-drive/core](https://github.com/tags-drive/core) - contains backend part (written in **Go**)
- [tags-drive/web](https://github.com/tags-drive/web) - contains web part (written in **Vue.js** and **TypeScript**)
- [tags-drive/scripts](https://github.com/tags-drive/scripts) - contains scripts for the deployment
