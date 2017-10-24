# Consul Practice Cluster

Featuring:
- Consul
- Consul Template

## Cluster Up
```bash
docker-compose up -d
```

## Version:
```bash
docker exec -it consulpractice_consul-template_1 consul-template --version
consul-template v0.19.0 (33b34b3)
```

## Consul Dashboard:
http://localhost:8500


## Add a data item to Consul
```bash
docker exec -it consulpractice_consul1_1 consul kv put foo bar
```

(Data in the UI: http://localhost:8500/ui/#/dc1/kv/)

## View the generated template
```bash
cat generated_template/out.txt
```

You can't tail because if the file is held open Consul-template can't update it.

If you want to "tail", try this in another terminal:

```bash
while true; do clear; cat generated_template/out.txt; sleep 1; done
```

and then just update the data:

```bash
docker exec -it consulpractice_consul1_1 consul kv put foo lolz
```


## Update the data
```bash
docker exec -it consulpractice_consul1_1 consul kv put foo yay_bar
```

## View the updated generated template 
```bash
cat generated_template/out.txt
```

## Cluster Down
```bash
docker-compose down
```

## Cleanup
```bash
docker ps -a | grep consul | awk '{ print $1 }' | xargs docker rm
rm -f generated_template/out.txt
docker rmi consul
```
