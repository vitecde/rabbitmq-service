# rabbitmq-service
Usage:

docker run -it -p 5672:5672 -p 15672:15672 --name worker_vitec --rm vitecde/rabbit-service

docker-compose.yml

crawler:
   image: vitecde/metadata-crawler
   volumes:
     - /c/Users/mchavarria.COMO-INTRA/workspace/myDocker:/crawler/videos
   links: 
    - rabbitService
   environment:
     - API_KEY=AIzaSyB3ezw4-Py8SfEvoOFuDrHrut4KrZrjosc
     - Q_PASSWORD=guest
     - Q_USER=guest
     - Q_NAME=crawlerQueue
     - Q_PORT=5672
     - Q_IP=rabbitService
   entrypoint: ./start_crawler.sh "SEARCH"

rabbitService:
    image: vitecde/rabbit_service
    ports:
    - "5672:5672"
    - "15672:15672"