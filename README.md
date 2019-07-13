# Tags Drive

**Tags Drive** is an open source standalone cloud drive. The main feature of **Tags Drive** is no folders. Instead, every file can have a tag (or tags).

![GitHub release](https://img.shields.io/github/release/tags-drive/core.svg?style=flat-square&label=Backend%20version)
![GitHub release](https://img.shields.io/github/tag-pre/tags-drive/core.svg?style=flat-square&label=Backend%20beta-version)

![GitHub release](https://img.shields.io/github/release/tags-drive/web.svg?style=flat-square&label=Frontend%20version)
![GitHub release](https://img.shields.io/github/tag-pre/tags-drive/web.svg?style=flat-square&label=Frontend%20beta-version)

---

- [Why I should prefer Tags Drive to other cloud drives](#Why-I-should-prefer-Tags-Drive-to-other-cloud-drives)
- [Installation](#Installation)
  - [Requirements](#Requirements)
  - [Running](#Running)
- [FAQ](#FAQ)
  - [What is the View Mode](#What-is-the-View-Mode)
  - [How to upload new files](#How-to-upload-new-files)
  - [How to preview files](#How-to-preview-files)
  - [How to search files](#How-to-search-files)
  - [How to select multiple files](#How-to-select-multiple-files)
  - [How to manage files](#How-to-manage-files)
  - [Can I share files](#Can-I-share-files)
  - [Trash](#Trash)
  - [Other](#Other)
- [Infrastructure](#Infrastructure)

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

## FAQ

### What is the View Mode

There're 2 **View Modes**:

- **Cards**
- **List**

You can switch them in **Settings**

### How to upload new files

You can upload new files with **Drag and Drop**

### How to preview files

You can open the **Preview Window** with click on a file image. You can switch previews by arrows.

### How to search files

**Tags Drive** provides search with logical expression. You can use logical operators:

- `!` – logical NOT
- `&` – logical AND
- `|` – logical OR
- `(`, `)`

For example, you have tags with id `1`, `5`, `23`. You want to find files with tags `1` and `5` and without `23`, but files must not have tags `1` and `5` at the time. You can use next search request: `!(1&5)&!23`

Additional information about logical algebra on Wikipedia: [Boolean algebra](https://en.wikipedia.org/wiki/Boolean_algebra)

### How to select multiple files

You can select multiple files with **Ctrl+Left Button**

### How to manage files

You can open **Context Menu** on **Right Button**.

### Can I share files

Yes, you can share files from **Context Menu**. You can manage **Share Tokens** from **Settings**.

### Trash

There are 2 ways to delete a file

- **Trash**: you can move a file into Trash. Then file will be deleted after 1 week.

- **Force delete**: you can delete a file immediately

### Other

- You can keep files with same filenames
- You can tag files before upload on **Upload Window**
- You can sort files by name, size and adding time

## Infrastructure

There are several repositories:

- [tags-drive/core](https://github.com/tags-drive/core) - contains backend part (written in **Go**)
- [tags-drive/web](https://github.com/tags-drive/web) - contains web part (written in **Vue.js** and **TypeScript**)
- [tags-drive/scripts](https://github.com/tags-drive/scripts) - contains scripts for the deployment
