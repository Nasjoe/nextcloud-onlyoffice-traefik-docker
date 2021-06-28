# nextcloud-onlyoffice-traefik-docker
A Docker stack for Nextcloud with Onlyoffice behind Traefik, with https !


Change .env variable.

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
allow to set onlyoffice as local conainer. Within the nextcloud contener :
```
sudo -u www-data sh -c "php occ --no-warnings config:system:set allow_local_remote_servers --value=true"
```

