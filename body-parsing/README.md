### Body Parse

#### run it:

```shell
node --harmony app.js
```

#### using curl:

```shell
$ curl -X POST -d '{"name": "tangzhixiong"}' http://localhost:3000
.name required                                                                                                                                                                         $ 
$ curl -H "Content-Type: application/json" -X POST -d '{"name": "tangzhixiong"}' http://localhost:3000
{"name":"TANGZHIXIONG"}
```
