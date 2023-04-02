##  Deploy Docker application on a server with Docker Compose

### Technologies used:
Docker, Amazon ECR, Node.js, MongoDB, MongoExpress

### Project Description:

Copy Docker-compose file to remote server
Login to private Docker registry on remote server to fetch our app image
Start our application container with MongoDB and MongoExpress services using docker compose

### Below are the steps to deploy a Docker application on a server with Docker Compose:

Step 1: First, make sure that we have Docker and Docker Compose installed on your local machine.

Step 2: Create a Docker Compose file that defines your application and its dependencies. Here's an example Docker Compose file for a Node.js app with MongoDB and MongoExpress services:

        version: '3'
    services:
      my-app:
        image: 568534212756.dkr.ecr.ap-south-1.amazonaws.com/my-app:1.0
        ports:
          - 3000:3000
      mongodb:
        image: mongo
        ports:
          - 27017:27017
        environment:
          - MONGO_INITDB_ROOT_USERNAME=admin
          - MONGO_INITDB_ROOT_PASSWORD=password
      mongo-express:
        image: mongo-express
        ports:
          - 8080:8081
        environment:
          - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
          - ME_CONFIG_MONGODB_ADMINPASSWORD=password
          - ME_CONFIG_MONGODB_SERVER=mongodb

Step 3: Build Docker image and push it to private Docker registry. You can use the following commands to build and push your Docker image to Amazon ECR:

        docker build -t <your-docker-image-url> .
    docker push <your-docker-image-url>
       
Step 4: Copy the Docker Compose file to your remote server. You can use the scp command to copy the file to your server:

    scp docker-compose.yml <remote-server-username>@<remote-server-ip>:<remote-path>

Step 5: SSH into your remote server and log in to your private Docker registry using the following command:

    aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 568534212756.dkr.ecr.ap-south-1.amazonaws.com
    
Step 6: Navigate to the directory where you copied the Docker Compose file and run the following command to start your application:

    docker-compose -f mongo.yaml up
    
Step 7: Once the containers are up and running, you can access your application by navigating to the IP address of your remote server in a web browser. In this example, you would navigate to http://<remote-server-ip>:80 to access your Node.js application.

That's it! Your Docker application is now up and running on your remote server with Docker Compose.








 
