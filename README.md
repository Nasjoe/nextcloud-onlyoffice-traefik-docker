# nextcloud-onlyoffice-traefik-docker
A Docker stack for Nextcloud with Onlyoffice behind Traefik, with https !


create frontend and database network

```
docker network create --driver=overlay frontend
docker network create --driver=overlay database
```

Start Traefik :
```
docker-compose -f docker-compose-traefik up -d
```

Start Nextcloud Stack
```
docker-compose up -d
```

Configure Nextcloud.