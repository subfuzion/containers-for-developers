---
description: docker run
---

# Launch a container

To launch a container with the `hello` image you created, enter the following command:

```text
docker run --name demo --rm -it hello
```

You should see the following output:

```text
Hello, world!
```

Try supplying an argument:

```text
docker run --name demo --rm -it hello friend
```

Output:

```text
Hello, friend!
```

### Command explanation

The command may look a bit intimidating at first, but these are all very standard options for working at the command line. Let's break this command down.

#### docker run

`docker run` is used to launch containers. At the very least, the command needs to know what image to use to create the container to run it:

```text
docker run hello
```

If you run this, the command will still work. So why did we need all the extra options?

If you run the following command:

```text
docker container ls
```

You shouldn't see any containers running right now \(at least not the `hello` container\).

But if you run the same command with the `-a|--all` option:

```text
docker container ls -a
```

You should see something like this:

```text
CONTAINER ID   IMAGE     COMMAND          CREATED         STATUS                     PORTS      NAMES
6b923562d648   hello     "/hello.sh"      3 minutes ago   Exited (0) 3 minutes ago              exciting_euclid
```

What this means is that even though the command exited when finished, the container is still taking up resources on your system. Since you can't use the container anymore, generally the only reason you want to do this is if you want to keep the container around so you can inspect its logs \(whatever it printed as output to `stdout` or `stderr`\).

So let's try that. Unfortunately, since you didn't supply the `--name` option, you can't refer to the container by a name you chose, so you'll need to refer to it either by the name that Docker chose for you \(in this case, `exciting_euclid`\) or by its container ID \(you only need a non-ambiguous portion of it, like: `6b92`\).

```text
docker logs 6b92
```

You should see the output that was printed when the program ran:

```text
Hello, world!
```

Let's go ahead and clean up; we'll need to manually remove the container now that we're finished with it:

```text
docker container rm 6b92
```

You'll see confirmation that it was removed:

```text
6b92
```

And if you want, you can confirm by entering `docker container ls -a` again.

#### The --name option

As you can see, naming your containers is a good practice. It makes it easy to perform commands on it. Most of the time that you don't name your container, you'll end up wishing you did. The only time you really can't name your containers is when you will be launching multiple copies of a container in parallel.

#### The --rm option

To avoid the problem of dead containers hanging around, `--rm` option is another option you should get into the habit of using. All this option does is tell Docker to automatically clean up for you when the container exits \(technically when the process running as PID 1 exits inside of the container\).

Generally the only time you don't want to do this is if you want to keep the container around to inspect its logs, maybe because the container keeps stopping because the PID 1 process is crashing.

#### The -it options

Note that `-it` is just a grouping of two short options \(hence the single dash instead of the double dash used by the long options\). The two short options are:

* `-i` - interactive; in a nutshell, this allows you to send input from `stdin` \(normally your keyboard\) to the process in the container.
* `-t` - this is the short option for `--tty`, which attaches a \(virtual, or pseudo\) terminal to the process in the container. What this means is that you can send signals from the terminal \(such as `SIGINT` with `CTRL-C`\) to the process and the process can output formatted output, such as ANSI color escape codes without it being printed as garbage on your screen \(see this [example](https://learning.oreilly.com/library/view/linux-shell-scripting/9781785881985/b0ddd805-aa79-441d-b5a7-380c66c7712d.xhtml) from O'Reilly\).

You will almost **always** want to use the two options together for containers that you run from your terminal in the foreground. In this case, the `hello` container runs and exits right away, so you don't need to signal it to quit, and you don't need to keep `stdin` attached so you can provide input to the running program, but you will use `-it` so often when working with containers interactively, you might as well just get used to entering it.

