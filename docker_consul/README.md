# setup file config
```bash
mkdir -p /interation/consul
mkdir -p /interation/consul/data
vi /interation/consul/config/consul-config.json
```
# docker compose
```bash
vi docker-compose.yml
```
# run docker
```bash
docker-compose up -d
```
# login container
```bash
docker exec -it aca218ca0a5d sh
```