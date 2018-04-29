This document is about how to write a node.js application, how to containerize it with jaeger and how to deploy it in Kubernetes as a service on MOC.

1 Install Node.js

2 Install NPM and Express Framework

	mkdir helloworld 
	cd helloworld
	npm init 

3 Add Express Framework as the first dependency

	npm install express --save

  The file should look like this:
	{
	  "name": "helloworld",
	  "version": "1.0.0",
	  "description": "",
	  "main": "index.js",
	  "scripts": {
 	   "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "author": "",
	  "license": "ISC",
	  "dependencies": {
	    "express": "^4.15.2"
	  }
	}

4 Run the app

	node index.js

  Go to http://localhost:8081/ in your browser to view it.


5 Dockerizing node.js application

  Add Dockerfile to the applications directory.
  The Dockerfile should look like this:

	FROM node:7
	WORKDIR /app
	COPY package.json /app
	RUN npm install
	COPY . /app
	CMD node index.js
	EXPOSE 8081

6 Build Docker image

	docker build -t hello-world .

7 Run Docker container

	docker run -p 8081:8081 hello-world

  You can also share your docker image if you want. But this document doesn't cover this.

8 Use kubectl to run Docker image
	
  List all Docker images
	
	docker ps
  
  Start the pod running the application
	
	kubectl run --image=<image name> <deployment name> --port=80 --env="DOMAIN=cluster"

  Expose a port through with a service

	kubectl expose deployment <deployment name> --port=80 --name=<service name>

  Now you are all set. Use
	
	kubectl get services
  
 to check the service.

  

  
