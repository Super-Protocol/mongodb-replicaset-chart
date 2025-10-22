## Install
```bash
helm -n justtest2 upgrade -i test mongodb-replicaset-chart --create-namespace
```

## Test
```bash
kubectl -n justtest2 run  my-mongodb-client --rm --tty -i --restart='Never' --image mongo:7.0 --command -- mongosh 'mongodb://root:bf430fd8d529b5ab5ce639fa33@mongodb-0/admin?ReplicaSet=rs0&directConnection=true'
```

## ToDo
- Add job for fix autodiscovery IP
