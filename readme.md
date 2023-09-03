Build first utility container

Create  a Empaty Folder and create Dockerfile 

FROM node:18
WORKDIR /app

then build the image using 
$ docker build -t node-util .
Run Container and bing the source folder
$ docker run -it -v /Users/macbookair/Desktop/dockerProject/docker-complete-utility:/app node-util npm init

give the answer of npm init

now if you do docker ps container is not running beasuse the container is just created there is nothing to run the npm is just initalize and if you want to install in dependecy in the container use cmd

$ docker run -it -v /Users/macbookair/Desktop/dockerProject/docker-complete-utility:/app node-util install

Entrypoint 

ENTRYPOINT ["npm"]

now build the image
$ docker build -t mynpm .
$ docker run -it -v /Users/macbookair/Desktop/dockerProject/docker-complete-utility:/app mynpm init

$ docker run -it -v /Users/macbookair/Desktop/dockerProject/docker-complete-utility:/app mynpm install

after running the command you can see you have package.json and package-lock.json files

now delete the lock file and install express with docker run

$ docker run -it -v /Users/macbookair/Desktop/dockerProject/docker-complete-utility:/app mynpm install express

now see you have node_modules and lock file both with express dependency


now using docker compose how to build utility container


docker-compose.yaml

version: '3.9'
services:
  npm:
    build: ./
    stdin_open: true
    tty: true
    volumes:
      - ./:/app

now run docker-compose up but it will not work 
so use docker-compose run npm init      
or if you want to delete after execute the compose 
use docker-compose run --rm npm init 