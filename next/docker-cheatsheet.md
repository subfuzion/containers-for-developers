---
description: Use this cheatsheet while going through the repo examples
---

# Docker cheatsheet



Docker command-line reference [https://docs.docker.com/engine/reference/commandline/](https://docs.docker.com/engine/reference/commandline/)

## Run a container in the background

```text
docker run -d --name NAME IMAGE[:TAG] [CMD] [OPTS...]
```

## Run a container interactively

```text
docker run -it --rm --name NAME IMAGE[:TAG] [CMD] [OPTS...]
```

or

```text
docker run -it --rm --name NAME --entrypoint CMD IMAGE[:TAG] [OPTS...]
```

Options

* `-it` - these are two short options joined together:
  * `-i` for "interactive" \(read from STDIN, keep open even when not attached\)
  * `-t` for TTY \(attaches a pseudo-TTY, which makes interaction inside container behave like a normal terminal session\)
* `--rm` - automatically remove the container when it exits \(generally when the process running as PID 1 terminates\), so that the stopped container no longer consumes resources on the host system
* `--name NAME` - generally a good idea to name the container since it makes it easier to reference it from other commands
* `--entrypoint` - use this if you want to run a custom command and specifying CMD shown the first way doesn't work

### Detaching and reattaching to a running container

Press the following key sequence to detach: `CTRL-P,CTRL-Q`

You will then be detached from the container \(you may see `read escape sequence` printed\) and returned to the prompt.

To reattach to the container, enter: `docker attach CONTAINER`

Many users find it convenient to override the default key sequence. One reason is that the default sequence interferes with using `CTRL-P` to scroll through previous commands if you're using a shell in an attached terminal. See [here](https://docs.docker.com/engine/reference/commandline/attach/#override-the-detach-sequence) for details.

## View output from a running container

```text
docker logs -f CONTAINER
```

`-f` option is used to continuously "follow" log output \(like the Unix `tail` command\).

Run `docker help logs` to see other useful options.

## Overriding a containers entrypoint

The image for a container might specify an entrypoint. This changes the behavior of the `docker run` command slightly and is generally done for running containers that should behave as dedicated tools. Anything specified after IMAGE is not used to run a command in the container, but is instead passed as options to the defined entrypoint command.

Sometimes, however, you want to be able to override the default entrypoint and specify the command to run the way you can with containers that don't have defined entrypoints. You can do this with the `--entrypoint` option.

```text
docker run --entrypoint CMD IMAGE[:TAG] [OPTS...]
```

