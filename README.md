## This app shows a simple user profile app set up using
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage
### All components are docker-based
### //NOTE: Works on temporary container storage as volume not attached.
## Part 1: With Docker
To start the application
## Step 1: Create docker network
```
$ docker network create mongo-network
```
## Step 2: start mongodb
```
$ docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo
```
## Step 3: start mongo-express
```
$ docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express  
```
## NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit --net flag in docker run command
## Step 4: open mongo-express from browser
## Link: http://localhost:8081
## Step 5: create my-db database and users collection using mongo-express (mongo-db UI)
## Step 6: Start your nodejs application locally - go to app directory of project
```
$ npm install 
$ node server.js
```
## Step 7: NodeJS application is now running. View UI in browser at port 3000.
## Link: http://localhost:3000
## Part 2: With Docker Compose: part of Infrastructure as a Code (IaaC), provisioning and running containers over a default network using docker compose file.
## To start the application
## Step 1: start mongodb and mongo-express
```
$ docker-compose -f docker-compose.yaml up
```
You can access the mongo-express under localhost:8080 from your browser

## Step 2: in mongo-express UI - create a new database "my-db"
## Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"
## Step 4: start node server
```
$ npm install 
$ node server.js
```
## Step 5: access the nodejs application from browser
### http://localhost:3000
## Using Dockerfile to build a docker image from the application:
```
$ docker build -t my-app:1.0 .
```
### The dot "." at the end of the command denotes location of the Dockerfile.
