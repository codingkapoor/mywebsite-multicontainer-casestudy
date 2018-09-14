# mywebsite-multicontainer-casestudy
Multi-Container System Design: A Case Study

# Step 1: Setup Ghost Backup

This will launch whitelisting based selective sync as container.
```
docker-compose -f docker-compose-dropbox.yml up -d
```

To register host with Dropbox follow the link provided in the logs.
```
docker logs -f mywebsite-multicontainer-casestudy_dropbox_1
```

Make sure data sync is complete before launch ghost blog in the next up. This is essential because all the data needs to be written to the docker volume created in the first step before this volume is attached to the ghost blog.
```
docker exec -it mywebsite-multicontainer-casestudy_dropbox_1 dropbox status
docker exec -it mywebsite-multicontainer-casestudy_dropbox_1 dropbox exclude
docker exec -it mywebsite-multicontainer-casestudy_dropbox_1 find ghost
```

# Step 2: Launch Website

This will launch reverse proxy, skdotcom and technology ghost blog as containers.
```
docker-compose -f docker-compose-mywebsite.yml up -d
```
