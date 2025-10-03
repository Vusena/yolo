# Overview
This project involved the containerization and deployment of a full-stack yolo application using Docker.


# Requirements
Install the docker engine here:
- [Docker](https://docs.docker.com/engine/install/) 

## How to launch the application 


![Alt text](image.png)

## How to run the app
Use vagrant up --provison command


Installing mongo db locally 

Downloaded the .deb file (e.g., mongodb-org-server_8.2.0_amd64.deb),
#Installing mongodb 
- cd Downlaods
- sudo dpkg -i mongodb-org-server_8.2.0_amd64.deb 
# Checking the status of mongodb 
- sudo systemctl status mongod.service
- sudo systemctl start mongod.service

#Downloading mongodb shell
-sudo dpkg -i mongodb-mongosh_2.5.8_amd64.deb 
-mongosh

#Back the application
-I ran node server.js
-Mongoose automatically connects to MongoDB at localhost:27017/yolomy.

# To fire up the client
-cd client/
-npm install 
-npm start
-if you encounter this error ---> Error: error:0308010C:digital envelope routines::unsupported
 try this command instead 
 -export NODE_OPTIONS=--openssl-legacy-provider
 -npm start