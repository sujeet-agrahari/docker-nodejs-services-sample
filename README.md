# Docker NodeJS Services Sample
Two sample NodeJS applications deployed in a private registry that run into two separate containers that share a queue

## Requirements
- Docker and Docker Compose

## Setup
First you have to run a private docker registry container:

```sh
docker run -d -p 5000:5000 --restart always --name registry registry:2
```
Then you have to create the services builds and push them into the local private registry:

```sh
cd ./consumer
npm run publish
cd ../producer
npm run publish
cd ..
```

## Run the stack

After the setup you can run the stack with docker compose:
```
npm run stack:start
```

## Try the stack

1. With your browser go to `http://localhost:8000`
2. Write something in the input box and press `Push to Queue`
3. You will see in the stack logs something like:
   ```
    producer_1  | producing "Something on the queue"
    consumer_1  | consumed msg:  Something on the queue
   ```