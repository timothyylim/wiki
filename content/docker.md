docker stop $(docker ps -aq) && docker system prune -af --volumes

docker-compose down -v
docker-compose up --build -d
