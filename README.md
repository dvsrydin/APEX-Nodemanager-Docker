# APEX-Nodemanager-Docker
Docker deployment for the APEX-Nodemanager application
### Configuration
You can configure your deployment inside the docker-compose.yml
### Build & Start
docker-compose up -d --force-recreate
### Reset (Delete) Containers
docker-compose down -v
### Start
docker-compose start
### Stop
docker-compose stop
### See container logs
docker logs -f nodemanager
### Bash into container
docker exec -it nodemanager /bin/bash