---
description: Dockerfile - line 3
---

# ENTRYPOINT

#### Dockerfile line 3

`FROM alpine`

This instruction tells Docker to use [alpine](https://hub.docker.com/_/alpine) as the base image for the image you're going to create. The base image provides a very lightweight distribution for Linux, called [Alpine](https://alpinelinux.org/).

We need a Linux distribution because we want to run a script using the Bourne shell \(`sh`\). Docker only uses the host Linux kernel, so if your container needs anything else, you're responsible for ensuring the image provides it. The `alpine` image includes `/bin/sh`, which our script depends on to run.

Although there are base images for all the major Linux distributions \(such as [debian](https://hub.docker.com/_/debian), [ubuntu](https://hub.docker.com/_/ubuntu), [centos](https://hub.docker.com/_/centos), etc\) that include `/bin/sh`, most of them include much more than what we need for such a simple program. Alpine Linux is often a good choice simple utilities and even some production applications.

#### Line 2

`COPY hello.sh /`

This instruction tells Docker to copy a file \(or files\) from **host** file system \(which in this case is your machine's file system\) to the destination directory in the **container** file system.

{% hint style="info" %}
You can only copy files from the directory containing your Dockerfile and any of its subdirectories.

You could have also written `/hello.sh` and this would still work since `hello.sh` is at the _root of your build context_, but making it look like an absolute path is confusing and unnecessary.
{% endhint %}

The **COPY** instruction can be used to **rename** the file. For example,

`COPY hello.sh /app`

would copy `hello.sh` to the root directory and rename it to `app`.

The following does **not** rename the file, but instead copies it to the `/app` directory \(and creates the directory if it doesn't exist\):

`COPY hello.sh /app/`

You can copy to any arbitrary path \(and it will be created\) **and** rename the file:

`COPY hello.sh /path/to/scripts/app.sh`

Finally, you can copy to destination paths that are relative to the current working directory, as specified using the `WORKDIR` instruction.

```text
WORKDIR /app
COPY hello.sh .
```

The path for `WORKDIR` does not need to exist. The `WORKDIR` instruction is useful when you need to run a number of commands in a specific directory.

#### Line 3

`ENTRYPOINT [ "/hello.sh" ]`

The `ENTRYPOINT` instruction 

