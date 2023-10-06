# Traefik

## Requirements
- [Docker](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/)

## Guide
1. Create a docker network to route from Traefik to your services.
```bash
sudo docker network create proxy
```

2. Deploy the config files and edit accordingly

3. Deploy the docker-compose.yml file
```bash
sudo docker compose up -d
```