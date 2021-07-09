---
description: >-
  Simple server app that responds with 'hello world' but only handles one route
  (the root URL: '/').
---

# demov1

### Terminal 1

If you have Node.js installed, you can run the app with these commands:

```text
npm install
npm start 
```

Output

```text
> demov1@1.0.0 start
> node app.js

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



