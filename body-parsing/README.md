### Body Parse

#### run it:

    node --harmony app.js


#### using curl:
    
    $ curl -X POST -d '{"name": "tangzhixiong"}' http://localhost:3000/uppercase                           
    .name required                                                                                                                                                                         $ 
    $ curl -H "Content-Type: application/json" -X POST -d '{"name": "tangzhixiong"}' http://localhost:3000/
    {"name":"TANGZHIXIONG"}                                                                 
