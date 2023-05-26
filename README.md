# fantom-docker
Docker image for Fantom Opera full node


This repo contains multiple components:
* A `docker-compose` setup which can launch a full-fledged API node. This consists of: 
    * `ingress` for an nginx instance running in front
    * `letsencrypt` for SSL certificates setup 
    * `opera` as the actual fantom opera node launch

* Individual docker components which can be built and launched on their own:
    * `opera`: uses pruned genesis, targeted for RPC and validator nodes
    * `opera_full`: for API nodes
    * `opera_snap`: for faster sync, targeted for RPC nodes
        

## Running an API node with `docker-compose` 

### Requirements

You need a Cloudflare account and a valid Cloudflare API key for the script to succeed.

You should also have a domain and host for your fantom node.

Create an `.env` file and set these values accordingly:

```sh
CLOUDFLARE_EMAIL=you@email.com (cloudflare account user)
CLOUDFLARE_API_KEY=cloudflare api key
FANTOM_HOSTNAME=fantom.yourdomain.com (for your fantom node)
```

### Run 

Use `docker-compose` and `docker` to interact with the containers

```sh
docker-compose up --build -d
```
 
# stop the node
```sh
docker-compose down
```
 
```sh
# view the logs
docker-compose logs -f
```
 
```sh
# start a shell in a new container with the same data volume
docker-compose run fantom ash
```

```sh
# attach to the go-opera json interface
docker-compose run fantom opera attach
```
 
```sh
# connect to the container
docker exec -it $(docker ps --filter "name=fantom" -q) ash
```
