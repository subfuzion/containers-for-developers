---
description: Dockerfile - line 1
---

# FROM

```text
FROM alpine
```

This instruction tells Docker to use [alpine](https://hub.docker.com/_/alpine) as the base image for the image you're going to create. The base image provides a very lightweight distribution for Linux, called [Alpine](https://alpinelinux.org/).

We need a Linux distribution because we want to run a script using the Bourne shell \(`sh`\). Docker only uses the host Linux kernel, so if your container needs anything else, you're responsible for ensuring the image provides it. The `alpine` image includes `/bin/sh`, which our script depends on to run.

Although there are base images for all the major Linux distributions \(such as [debian](https://hub.docker.com/_/debian), [ubuntu](https://hub.docker.com/_/ubuntu), [centos](https://hub.docker.com/_/centos), etc\) that include `/bin/sh`, most of them include much more than what we need for such a simple program. Alpine Linux is often a good choice simple utilities and even some production applications.

Docker will fetch this image from the machine's image cache when it comes time to build the image. If the image is not yet cached on this machine, Docker will automatically pull it from a remote image repository.

An image name can consist of a number of [components](https://docs.docker.com/engine/reference/commandline/tag/#extended-description) that can be used to indicate:

* The optional registry hostname where the image repository exists.
* The optional ID name to identify the location of the repository at the registry. Depending on the registry, this can be a user name, an organization name, a project ID, etc. If you need to specify the registry, then you will also need to specify this component.
* **The repository name for different versions of an image.**
* The optional tag name, which is used to distinguish logical versions of an image.

Without the tag component, Docker will add the `:latest` tag by default. If there is no version of the image published with the `:latest` tag, however, pulling the image will fail.

#### Image digest

An image can also be identified by **digest**, an immutable identifier when you want to pin to a specific version of a logical version of an image. A tag is a logical construct -- even if it looks like a version number, it only points to the latest version of an image that was pushed to the repository with that tag. Only using a digest **guarantees** that you will be using the exact image you intended to use.

A digest is only created when an image is pushed to a repository. Docker will print an image's digest when it is pushed or pulled from the command line. You can list digests for images on your machine with the following command:

```text
docker image ls --digests [NAME]
```

### Official images

In this case, the image is simply named `alpine`.

Without the registry component, this tells Docker that the registry is [Docker Hub](https://hub.docker.com/search?q=&type=image), a service provided by [Docker](https://www.docker.com/) for finding and sharing container images.

Without the ID name component, this tells Docker that the image is not under a user or organization account, but published as an [official image](https://docs.docker.com/docker-hub/official_images/).

Official images are images that have been curated by the Docker official images team, are considered the canonical images for a significant user community, exemplify best practices and provide clear documentation, are actively maintained and ensure that security updates are applied in a timely manner.

As you might expect, there are [official images](https://hub.docker.com/search?q=&type=image) for major [operating systems](https://hub.docker.com/search?q=&type=image&category=os), [programming languages](https://hub.docker.com/search?q=&type=image&category=languages), [servers](https://hub.docker.com/search?q=&type=image&category=application_infrastructure), [database servers](https://hub.docker.com/search?q=&type=image&category=database), and other significant applications and tools.



