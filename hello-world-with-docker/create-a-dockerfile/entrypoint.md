---
description: Dockerfile - line 3
---

# ENTRYPOINT

```text
ENTRYPOINT [ "/hello.sh" ]
```

The [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) instruction lets you configure a container that will run as as an executable. Every time you launch a container using this image, the container will run the program specified in `ENTRYPOINT`, and any options you provide when launching will be passed as arguments to the program.

Any **mandatory** command-line arguments for the the process should be specified after the program name. If specified, mandatory arguments will **not** be overridden by any explicitly supplied arguments when launching a container using this image.

For example:

{% tabs %}
{% tab title="exec form" %}
```text
ENTRYPOINT ["executable", "param1", "param2"]
```
{% endtab %}

{% tab title="shell form" %}
```
ENTRYPOINT command param1 param2
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Always use the **exec form**. There are significant disadvantages to using the **shell form**, discussed [here](https://docs.docker.com/engine/reference/builder/#entrypoint). In a nutshell, you want your process to run as PID 1 so that it can receive standard UNIX signals, particularly `SIGTERM`\(the conventional termination request signal\) and `SIGINT` \(triggered by `CTRL-C`\).
{% endhint %}

#### Optional arguments

Any **optional** command-line arguments that you would like to supply to the `ENTRYPOINT` process **by default** should be added to a [CMD](https://docs.docker.com/engine/reference/builder/#cmd) instruction. These will be appended to the list of any of mandatory arguments you specify with the `ENTRYPOINT` instruction. **However**, optional arguments **will** be overridden by any explicitly supplied arguments when launching a container using this image.

{% hint style="info" %}
The **CMD** instruction can be used by itself, not just to augment the **ENTRYPOINT** instruction, but to replace it. This is useful for launching containers where it's desirable to run different processes bundled in the image.  
  
When used this way, the first argument  for the CMD instruction must be the program to run, not one of the program options.

When launching a container, any supplied arguments will **replace** the entire CMD \(which, of course, means the first argument in this case must be the name of the program to run, followed by any other arguments\).
{% endhint %}



