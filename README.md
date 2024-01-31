Here's the comprehensive guide with all the provided Docker commands and explanations:

**Docker File Creation Commands**

1. Create a Dockerfile without any extension:  
   ```
   Dockerfile
   ```

2. Ensure that the `node_modules` folder does not exist at this time.

3. We need Node.js for running any React app. So, we have to write instructions in the Dockerfile for the installation of Node.js:
   ```
   FROM node
   ```

4. If we need a specific version of Node.js, we can add it as well:
   ```
   FROM node:20
   ```

5. Set up a working directory so that we can run our React app:
   ```
   WORKDIR /myreactapp
   ```

6. In an empty container, create the `myreactapp` folder responsible for our React app installations and other work.

7. Copy all work into the `myreactapp` folder:
   ```
   COPY . .
   ```

8. Run npm install command for the packages installation:
   ```
   RUN npm install
   ```

9. If we want to run our app on a different port, we can use this command:
   ```
   EXPOSE 3001
   ```

10. Command to run the Docker image:
    ```
    CMD [ "npm", "run", "dev" ]
    ```

**Make a Docker Image Command**

1. Make sure you are in your project directory and your Dockerfile will be saved. Then run this command in your terminal:
   ```
   docker build .
   ```

2. If we want to give a meaningful name to our Docker image or assign a tag to our image:
   ```
   docker build -t myfirstimage:01 .
   ```
   Note: `-t` assigns a version (01) and the name. It's useful for managing multiple versions of an app.

3. Remove an image by this command:
   ```
   docker rmi myfirstimage:01
   ```

**Basic Docker Commands**

1. If we want to see all images:
   ```
   docker image ls
   ```
   or
   ```
   docker images
   ```
   Note: We can run a single image in multiple containers because each container has its own space without conflict.

2. To create a container, we need the image id which is present in the previous command:
   ```
   docker run image_id
   ```

3. To see the running of all containers:
   ```
   docker ps
   ```
   To see all containers whether it's running or stopped:
   ```
   docker ps -a
   ```
   To remove multiple containers by adding space:
   ```
   docker rm container_name1 container_name2 container_name3
   ```

4. To stop any container:
   ```
   docker stop container_name
   ```
   Note: We can take the container name from the previous command or from Docker Desktop app.

5. Here is a problem - we have run our app but the browser does not know the container is running the app. So, we have to bind the port by this command:
   ```
   docker run -p 5173:5173 ff2ce433d9b1
   ```

6. To run the container in detach mode:
   ```
   docker run -d -p 5173:5173 ff2ce433d9b1
   ```

7. If we want the container to be removed automatically when stopped:
   ```
   docker run -d --rm -p 3002:5173 ff2ce433d9b1
   ```
   
8. If we want to give our container a name:
   ```
   docker run -d --rm --name "reactappcontainer" -p 3002:5173 ff2ce433d9b1
   ```

**Running multiple containers by a single image**

To achieve this, we have to assign different ports:
   ```
   docker run -d -p 3002:5173 ff2ce433d9b1
   ```
   ```
   docker run -d -p 3001:5173 ff2ce433d9b1 
   ```

**Running a Program with the Help of Terminal**

1. Suppose we have to run a Python program or PHP test case with the help of terminal and contraction:
   ```
   docker run -it image_name
   ```
   (Here `-it` means interactive terminal)

**Sharing Images on Docker Hub**

1. Firstly, create a repo on Docker Hub and then go to our local terminal and run this command:
   ```
   docker login
   ```
   (Enter username and password)

2. Recreate the new image with the name of your repo name like If I've created a repo and the command is (docker push vikaskumar0101/react-learning-app:tagname). So we need to recreate the image and the name should be this ( vikaskumar0101/react-learning-app:tagname).
   ```
   docker build -t vikaskumar0101/react-learning-app:tagname .
   ```
   Note: tagname you can replace with your version like 01, 02, etc.

3. Push the images on Docker Hub:
   ```
   docker push vikaskumar0101/react-learning-app:001
   ```

4. If you do not want to recreate the image, you can rename your image with the repo's name by this command:
   ```
   docker tag old_name:version new_name:version
   ```

**Docker Volume Related Command**

1. Suppose we have created a file and stored some information in that file. After running the container and stopping and running again, we notice we do not have old information because within the container, the program will perform file read and write operations. Once the container is stopped or removed, the file will be automatically deleted. Next time the container performs the same steps from start to end. To resolve this problem, Docker provides volume (storage).
   ```
   docker run -it --rm -v myvol1:/myreactapp/ imageid
   ```
   Note: Volume only present locally. To see related volume command:
   ```
   docker volume --help
   ```

**Docker External File Mount**

1. Suppose we have a file called `users.txt` and in this file, we have 10 records. After creating an image and running it into the container, we realize we have to add more data. This is not a good practice. To resolve this problem, we can mount or bind `users.txt` file with our local machine that has `users.txt` file by this command:
   ```
   docker run -v absolute_path_of_your_local_file:/myreactapp/user.txt --rm image_id
   ```
   
**Docker .dockerignore file**

1. If we do not want to send some folders or files in the Docker image like `node_modules` folder and `.git` folder, we can create a `.dockerignore` file and write folder and file names that we don't want to send.

**Communication between Containers**

1. Suppose we have a program that is taking data from an API, a web server, or a locally installed MySQL database. To resolve this situation, we will use the network concept of Docker.
   ```
   RUN composer require laravel/ui
   ```
   Note: This command should be in Dockerfile.


   ```
   host:"host.docker.internal"
   ```
   (It should be our hostname to interact local DB to the container)
   ```
   docker inspect container_name
   ```
   (It's used for getting information of our container like IP network or gateway which is used for if we have one container where we have installed MySQL and the other container will perform some operation with the first container so we need the first container IP address and paste into the second container host value)

**Docker Network**

1. Suppose we have two containers: one responsible for MySQL and another for our React app. We have to connect each other but the problem is we have to find the IP address of the first container and replace it in the other container's host value, and we have to create an image. To resolve this problem, Docker provides Docker network. We can create a network and bind both containers in this network and simply we have to give the first container name in the host value.
   ```
   docker network --help
   ```
   ```
   docker network create my-net
   ```
   (Here my-net is your network name)
   ```
   docker network ls
   ```
   (To see network lists)
   ```
   docker run -d --env MYSQL_ROOT_PASSWORD="root" --env MYSQL_DATABASE="userinfo" --name mysqldb --network my-net mysql
   ```
   (Here we are running mysqldb 2nd container and bind into my-net network)
   ```
   docker run -it --rm --network my-net b9b6a3facc24
   ```
   (Here we are running the first container and bind into the my-net network, and make sure you have replaced the host name by the first container name and create a new image and bind with the my-net network)
