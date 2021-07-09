---
description: Dockerfile - line 2
---

# COPY

```text
COPY hello.sh /
```

This instruction tells Docker to copy a file \(or files\) from the source **host** file system \(which in this case is your machine's file system\) to the destination directory in the **container** file system.

{% hint style="info" %}
You can only copy files from the source directory containing your Dockerfile and any of its subdirectories.

You could have also written `/hello.sh` and this would still work since `hello.sh` is at the _root of your build context_, but making it look like an absolute path unnecessary and potentially confusing.
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

#### 

