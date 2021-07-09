# Create a "Hello, World!" program

## Create a "Hello, World!" program

Create a "Hello, World!" program as a simple shell script. It will print a greeting for the name you provide as a command argument \(or default to "World"\).

{% code title="hello.sh" %}
```bash
#!/bin/sh

NAME=${1:-World}
echo "Hello, $NAME!"
```
{% endcode %}

Make it executable and confirm that it works as expected.

```bash
$ chmod +x hello.sh
$ ./hello.sh
```

Output:

```bash
Hello, world!
```

