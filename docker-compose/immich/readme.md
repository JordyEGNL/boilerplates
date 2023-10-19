# Immich

[Immich GitHub](https://github.com/immich-app/immich)

## Requirements
- [Docker](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/)

## Info
- Immich data is stored in a folder on the system, same for pgdata. Other data is stored in a docker volume
- Advised to use reverse proxy (I use Traefik) to add https support

## Guide
1. Deploy the config files and edit accordingly (.env file)

2. Make sure that the docker network "immich" exists. If you use Traefik as a reverse proxy add the proxy network to the immich-proxy container.
```bash
sudo docker network create immich
```

3. Deploy the docker-compose.yml file
```bash
sudo docker compose up -d
```