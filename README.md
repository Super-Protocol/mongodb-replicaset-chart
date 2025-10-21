## Install
```bash
helm -n justtest2 upgrade -i test test
```

## TODO
```bash
kubectl -n justtest2 exec -it mongodb-0 -- bash

mongosh --host 127.0.0.1 --quiet <<'JS'
rs.initiate({
  _id: "rs0",
  members: [
    { _id: 0, host: "mongodb-0.mongodb:27017" },
    { _id: 1, host: "mongodb-1.mongodb:27017" }
  ]
})
JS

mongosh --host 127.0.0.1 --quiet <<'JS'
use admin
db.createUser({ user: "root", pwd: "bf430fd8d529b5ab5ce639fa33", roles: ["root"] })
JS
```

## Test
```bash
kubectl -n justtest2 run  my-mongodb-client --rm --tty -i --restart='Never' --image mongo:7.0 --command -- bash
mongosh 'mongodb://root:bf430fd8d529b5ab5ce639fa33@mongodb-0,mongodb-0/admin?ReplicaSet=rs0'
```
