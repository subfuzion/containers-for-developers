---
description: Running the server in a container
---

# demov2



### Terminal 1

Build the image, launch a container:

```text
docker build -t demo .
docker run --name demo --rm -it -p 8080:8080 demo
```

Output

```text
server listening on :8080
```

### Terminal 2

```text
curl localhost:8080
```

Output

```text
<h1>hello world</h1>
```

Check logs

```text
docker logs demo
```

Output

```text
server listening on :8080
GET / 200 1.488 ms - 20
```

### Terminal 1

```text
docker rm -f demo
```

