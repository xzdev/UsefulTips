- Remove the containers that are not running
```
docker rm `docker ps -aq -f status=exited`
```