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
Go inside the container :
```
docker exec -u www-data -ti <nextcloud app container> bash
```

allow to set onlyoffice as local container. Within the nextcloud container :
```
php occ --no-warnings config:system:set allow_local_remote_servers --value=true
```

add hostame container and domain to trusted domain :
```
php occ --no-warnings config:system:set trusted_domains 1 --value="onlyoffice"
php occ --no-warnings config:system:set trusted_domains 2 --value="nextcloud"
php occ --no-warnings config:system:set trusted_domains 3 --value="<YOUR NEXTCLOUD_DOMAIN>"
php occ --no-warnings config:system:set trusted_domains 4 --value="<YOUR ONLYOFFICE DOMAIN>"
```

go to your nextlcoud instance, install it, go to app and add Onlyoffice from the app store.
Configure it

```
php occ --no-warnings config:system:set onlyoffice DocumentServerUrl --value="http://<ONLYOFFICE.DOMAIN>"
php occ --no-warnings config:system:set onlyoffice DocumentServerInternalUrl --value="http://onlyoffice/"
php occ --no-warnings config:system:set onlyoffice StorageUrl --value="http://nextcloud/"
php occ --no-warnings config:system:get onlyoffice
php occ onlyoffice:documentserver --check
```
