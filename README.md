# Tags Drive

**Tags Drive** is an open source standalone cloud drive. The main feature of **Tags Drive** is that files have flat structure (there's no folders). Instead, every file has a tag (or tags).

## Wiki

There's a [wiki document](WIKI.md).

## Why should I prefer Tags Drive to other cloud drives

For example, you want to save an image of a cat. You can save it into folder `cats` or into folder `cute`. Of course, you may keeps 2 equal files, but it would be better to use tags system. So, you just need to add tags `cats` and `cute` to the photo.

## Installing

**Requirements:**

- Docker

Run `docker pull kirtis/tags-drive`. Create `run.sh` to run docker container.

Example:

```sh
#!bin/sh
# Example of run.sh script
docker run --rm -d \
--name tags-drive \
-p 80:80 \
-v /home/username/configs:/app/configs \
-v /home/username/data:/app/data \
-v /home/username/ssl:/app/ssl \
--env-file /home/username/tags-drive.env \
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

| Variable    | Default | Description                                                              |
| ----------- | ------- | ------------------------------------------------------------------------ |
| PORT        | 80      | Port for website                                                         |
| TLS         | true    | Should **Tags Drive** use https                                          |
| LOGIN       | user    | Login                                                                    |
| PSWRD       | qwerty  | Password                                                                 |
| ENCRYPT     | false   | Should the **Tags Drive** encrypt uploaded files                         |
| DBG         | false   |                                                                          |
| SKIP_LOGIN  | false   | Let use **Tags Drive** without auth (only for debug)                     |
| PASS_PHRASE | ""      | Passphrase is used to encrypt files. It can't be empty if `ENCRYPT=true` |

## Infrastructure

There are several repositories:

- [tags-drive/core](https://github.com/tags-drive/core) - contains backend part (written in **Go**)
- [tags-drive/web](https://github.com/tags-drive/web) - contains web part (written in **Vue.js**)
- [tags-drive/scripts](https://github.com/tags-drive/scripts) - contains scripts for deployment