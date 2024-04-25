# JAYP0710.github.io
To run Three Tier Application using Docker, we need to first create a Full Stack Project. We can use any of our Full Stack Project but if we don’t have one then we can use someone else project also. Here, I have used a very easy simple project on GitLab.This project is made using HTML, CSS, JavaScript, Express and MongoDB.<br>
First you need to clone the Project Repository from the link using command:
git clone https://gitlab.com/nanuchi/developing-with-docker <br>
To run a Three Tier Application, we need to run three Docker Containers simultaneously. So, it is necessary to run all these containers inside a network to avoid their interaction with other containers. 
So, Network can be created by using the following command after starting the Docker Engine with name mongo-network<br>
![image](https://github.com/JAYP0710/JAYP0710.github.io/assets/168062645/f1aadd96-f318-4c8e-821b-e0e1df589229)
<br>
You can see all the networks using the command: docker network ls. Now, we need to pull the image of MongoDB from DockerHub and make container from it. Then we need to run this container in the network to access MongoDB Database using Docker Container.<br>
![image](https://github.com/JAYP0710/JAYP0710.github.io/assets/168062645/294dc3a8-6a2b-434b-86d3-c9bbe98ed0d1)
<br>
To pull MongoDB image from DockerHub and run it as container we need to execute the command
![image](https://github.com/JAYP0710/JAYP0710.github.io/assets/168062645/d1fe79a0-8d51-4332-8ba4-e6081e28727a)
<br>
Here, the mongo image will be automatically pull from the DockerHub to run the Container in detachable mode with name mongodb in the network mongo-network. The Container will be running on the default 27017 port. You can check all the running containers using command docker ps. Environment Variables Username and Password are also passed to run the container. Similarly, we will be creating another container of Express by pulling its image from the DockerHub.
Express Container can be run by using the follow command
![image](https://github.com/JAYP0710/JAYP0710.github.io/assets/168062645/b016f3cb-f417-45bb-b44c-4359d48cb470)
<br>
Here, the container with name mongo-express is made to connect the MongoDB Database with the Frontend of the project in Docker. As explained above, the container will run on 8081 port. The environment variables Username and Password are passed of the MongoDB to access the Database along with the container name of the MongoDB in the Server Environment variable. The container will be running on the same network as the above container.
Now, open the link in your browser localhost:8081 and create two databases my-db and user-accounts
<br>
Creating these two databases is necessary as the Frontend will be requiring these while running. Also, we need to change the MongoDB URL mentioned in the server.js file as we will be running MongoDB using Docker instead of Local Machine.
Naviagate to the server.js file in the project and replace mongoUrlLocal and mongoUrlDocker with the following value
<br>
create a new Dockerfile inside the app folder of the project with the following commands
FROM node WORKDIR /app COPY . . ENV MONGO_DB_USERNAME=admin ENV MONGO_DB_PWD=password RUN npm install EXPOSE 3000 CMD [“node”, “server.js”]<br>
Open the CMD Terminal inside the app folder of the project and run the command 
To run the Image as a Docker Container run the command
Now, open the following link on you browser localhost:3000 and you will see a webpage running.
To push the Docker Image of the project run the command
