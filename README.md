# APEX-Nodemanager-Docker
Docker deployment for the APEX-Nodemanager application
### Configuration
You can configure your deployment inside the docker-compose.yml
### Run
docker-compose up --build -d
### See container logs
docker logs -f nodemanager
### Bash into container
docker exec -it nodemanager /bin/bash
### Fresh install
docker-compose down && docker-compose build --no-cache && docker-compose up -d --force-recreate