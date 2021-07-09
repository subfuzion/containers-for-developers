---
description: docker build
---

# Build an image

Enter the following command:

```text
docker build -t hello .
```

You should see output like the following:

```text
[+] Building 8.2s (7/7) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                      0.0s
 => => transferring dockerfile: 98B                                                                                                                       0.0s
 => [internal] load .dockerignore                                                                                                                         0.0s
 => => transferring context: 2B                                                                                                                           0.0s
 => [internal] load metadata for docker.io/library/alpine:latest                                                                                          7.5s
 => [internal] load build context                                                                                                                         0.0s
 => => transferring context: 84B                                                                                                                          0.0s
 => [1/2] FROM docker.io/library/alpine@sha256:234cb88d3020898631af0ccbbcca9a66ae7306ecd30c9720690858c1b007d2a0                                           0.6s
 => => resolve docker.io/library/alpine@sha256:234cb88d3020898631af0ccbbcca9a66ae7306ecd30c9720690858c1b007d2a0                                           0.0s
 => => sha256:234cb88d3020898631af0ccbbcca9a66ae7306ecd30c9720690858c1b007d2a0 1.64kB / 1.64kB                                                            0.0s
 => => sha256:53b74ddfc6225e3c8cc84d7985d0f34666e4e8b0b6892a9b2ad1f7516bc21b54 528B / 528B                                                                0.0s
 => => sha256:b0e47758dc53e7391c7abf92fd56fd959bf37fb74574feba3d557b4182d15801 1.47kB / 1.47kB                                                            0.0s
 => => sha256:58ab47519297212468320b23b8100fc1b2b96e8d342040806ae509a778a0a07a 2.71MB / 2.71MB                                                            0.3s
 => => extracting sha256:58ab47519297212468320b23b8100fc1b2b96e8d342040806ae509a778a0a07a                                                                 0.2s
 => [2/2] COPY hello.sh /                                                                                                                                0.0s
 => exporting to image                                                                                                                                    0.0s
 => => exporting layers                                                                                                                                   0.0s
 => => writing image sha256:e9b13eecbdee4d14c1eca94d8a82442e338996d6f7b219c06c77e8259efe4597                                                              0.0s
 => => naming to docker.io/library/hello                                                                                                                  0.0s
```

Here's what happened when you ran the command:

* Docker parses the Dockerfile. If there are any errors, the build will exit with an error.
* Docker copies everything in the file system rooted at this directory level that isn't explicitly ignored in a [.dockerignore file](https://docs.docker.com/engine/reference/builder/#dockerignore-file) \(if you're familiar with `.gitignore` files, then you already know the format of a `.dockerignore` file\) to a unique working area in the file system that comprises the **build context**. Whatever makes it into the build context is available to be copied into the image.
* In the `=> [1/2]` step, Docker processes the first instruction. It determines that the `alpine` image is not stored in the machine's image cache, so it pulls it from Docker Hub. Each of the following lines until the next instruction reflect a layer of the `alpine` image that is being fetched and cached. There is a one-to-one correspondence between every instruction in a docker file and the layer that is generated. The image cache significantly improves fetch performance and well as reduces the amount of storage required when using images that share ancestor images.
* In the `=> [2/2]` step, Docker performs the `COPY` instruction, copying `hello.sh` from the build context into the image.
* Finally, in `=> exporting to image`, Docker creates the image and names it.

You can view the final result with the `docker image ls` command:

```text
docker image ls hello
```

Output:

```text
REPOSITORY   TAG       IMAGE ID       CREATED             SIZE
hello        latest    e9b13eecbdee   About an hour ago   5.33MB
```

You can inspect more details with the `docker inspect` command:

```text
docker image inspect hello
```

Output \(shortened for space\):

```text
[
    {
        "Id": "sha256:e9b13eecbdee4d14c1eca94d8a82442e338996d6f7b219c06c77e8259efe4597",
        "RepoTags": [
            "hello:latest"
        ],
        ...
        "ContainerConfig": {
            ...
        },
        "DockerVersion": "",
        "Author": "",
         "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": null,
            "Image": "",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/hello.sh"
            ],
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "arm64",
        "Os": "linux",
        "Size": 5328210,
        "VirtualSize": 5328210,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/a40acf88a9b6b9e6da066a8f2d1570d33048c93532f6cbac4a81a7f7a622acb4/diff",
                "MergedDir": "/var/lib/docker/overlay2/ocsq71zwj6d5f5vo5z8i8jdq8/merged",
                "UpperDir": "/var/lib/docker/overlay2/ocsq71zwj6d5f5vo5z8i8jdq8/diff",
                "WorkDir": "/var/lib/docker/overlay2/ocsq71zwj6d5f5vo5z8i8jdq8/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:5e04d10b60a48b2fef3614c8b2bf64312b03380ac01bcec220e16885fe660be5",
                "sha256:a5b554d4129b8dd741ac53baccd043787acfe934e693d995632da2cd34ce6e65"
            ]
        },
        "Metadata": {
            "LastTagTime": "2021-07-09T11:35:19.523634675Z"
        }
    }
]
```

The important things to note here to reinforce your understanding at this point are:

* **Config** - this defined the container's environment when it launches.
  * You can confirm here that the entrypoint for a container is `/hello.sh.`
* **ContainerConfig** - only mentioned to point out that every instruction in a Dockerfile actually runs in its own container while building each corresponding image layer; this is the Config for the "build" containers.
* **RootFS** - you can confirm here that the two instructions processed for writing to the image file system \(`FROM` and `COPY`\) resulted in the two layers of the file system.

Keep in mind that the container's file system, as composed by all the image layers, must in general provide all the file dependencies a containerized process will need when it runs -- it does not have access to the host's file system unless you explicitly mount a file or directory into it for certain types of scenarios \(such as a persistent cache\).



