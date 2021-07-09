# Create a Dockerfile

A [**Dockerfile**](https://docs.docker.com/engine/reference/builder/) is a text file that contains the commands used to assemble an image.

An **image** is what Docker uses to launch containers. It comprises the environment configuration and files that will be needed to run a particular application, above and beyond what is provided by the underlying host Linux kernel.

A **container** is a process \(or a set of processes\) that uses Linux features to run in an environment that is completely isolated \(hence containerized\) from other processes running on the system.

You write a Dockerfile to build an image so that you can launch containers with the confidence that each container will run in an identical environment exactly as specified, no matter where you run the container.

The Dockerfile for creating our hello image only requires a few instructions:

{% code title="Dockerfile" %}
```text
FROM alpine
COPY hello.sh /
ENTRYPOINT [ "/hello.sh" ]
```
{% endcode %}

These three instructions will be used to tell Docker what should go into the image we want to create.

The first instruction tells Docker that the **base image** for this image will be an image called `alpine`. This image contains a lightweight Linux distribution that includes the Bourne shell \(`sh`\), which we'll need to execute our script.

