# Create a Dockerfile

A **Dockerfile** is a text file that contains the commands used to assemble an image.

An **image** is what Docker uses to launch containers. It comprises the environment configuration and files that will be needed to run a particular application, above and beyond what is provided by the underlying host Linux kernel.

A **container** is a process \(or a set of processes\) that uses Linux features to run in an environment that is completely isolated from other processes running on the system.

The Dockerfile for creating our hello image only requires a few instructions:

{% code title="" %}
```text
FROM alpine
COPY hello.sh /
ENTRYPOINT [ "/hello.sh" ]
```
{% endcode %}

These three instructions will be used to tell Docker what should go into the image we want to create.

The first instruction tells Docker that the **base image** for this image will be an image called `alpine`. This image contains a lightweight Linux distribution that includes the Bourne shell \(`sh`\), which we'll need to execute our script.

