# Docker-Complete-Guide

**Docker File Creation Commands**

1. Create a Dockerfile without any extension:  
   ```
   Dockerfile
   ```

2. Ensure that the `node_modules` folder does not exist at this time.

3. Include Node.js installation instructions in the Dockerfile as we need Node.js to run any React app:  
   ```
   FROM node
   ```

4. Optionally, specify a specific version of Node.js:  
   ```
   FROM node:20
   ```

5. Set up a working directory for running our React app:  
   ```
   WORKDIR /myreactapp
   ```

6. In an empty container, create the 'myreactapp' folder responsible for React app installations and other work.

7. Copy all work into the 'myreactapp' folder:  
   ```
   COPY . .
   ```

8. Install packages using npm install:  
   ```
   RUN npm install
   ```

9. Optionally, specify a different port to run the app:  
   ```
   EXPOSE 3001
   ```

10. Command to run the Docker image:  
    ```
    CMD [ "npm", "run", "dev" ]
    ```

**Make a Docker Image Command**

1. Ensure you are in your project directory where your Dockerfile will be saved. Then, run this command in your terminal:  
   ```
   docker build .
   ```

2. Assign a meaningful name or tag to your Docker image:  
   ```
   docker build -t myfirstimage:01 .
   ```
   Note: '-t' assigns a version (01) and the name. It's useful for managing multiple versions of an app.

3. Remove an image with this command:  
   ```
   docker rmi myfirstimage:01
   ```

**Basic Docker Commands**

1. View all images:  
   ```
   docker image ls
   OR
   docker images
   ```
   Note: A single image can run in multiple containers, as containers have their own spaces without conflict.

2. Create a container using the image ID from the previous command:  
   ```
   docker run image_id
   ```

3. Check the running status of all containers:  
   ```
   docker ps
   docker ps -a
   ```

4. Remove multiple containers by specifying their names:  
   ```
   docker rm container_name1 container_name2 container_name3
   ```

5. Stop a container:  
   ```
   docker stop container_name
   ```

6. Bind the port to make the app accessible via a browser:  
   ```
   docker run -p 5173:5173 ff2ce433d9b1
   ```

7. Run a container in detach mode:  
   ```
   docker run -d -p 5173:5173 ff2ce433d9b1
   ```

8. Automatically remove the container when stopped:  
   ```
   docker run -d --rm -p 3002:5173 ff2ce433d9b1
   ```

9. Assign a name to the container:  
   ```
   docker run -d --rm --name "reactappcontainer" -p 3002:5173 ff2ce433d9b1
   ```

**Running Multiple Containers by a Single Image**

To achieve this, assign different ports:  
   ```
   docker run -d -p 3002:5173 ff2ce433d9b1
   docker run -d -p 3001:5173 ff2ce433d9b1
   ```
**Running a Program with the Help of Terminal**

1. Suppose we have to run a Python program or PHP test case with the help of terminal and docker:  
   ```
   docker run -it image_name
   ```
   (Here `-it` means interactive terminal)

**Sharing Images on Docker Hub**

1. Firstly, create a repository on Docker Hub and then go to our local terminal and run this command:  
   ```
   docker login
   ```
   (Enter username and password)

2. Recreate the new image with the name of your repository. For example, if I've created a repository and the command is:
   ```
   docker push vikaskumar0101/react-learning-app:tagname
   ```
   So we need to recreate the image and the name should be like this:
   ```
   docker build -t vikaskumar0101/react-learning-app:tagname .
   ```
   Note: Replace 'tagname' with your version like 01, 02, etc.

3. Push the images to Docker Hub:
   ```
   docker push vikaskumar0101/react-learning-app:001
   ```

4. If you do not want to recreate the image, you can rename your image with the repository's name using this command:
   ```
   docker tag old_name:version new_name:version
   ```

**Docker Volume Related Commands**

1. Suppose we create a file and store some information in that file. After running the container, stopping it, and running it again, we observe that we do not have the old information. This is because within the container, the program performs file read and write operations, and once the container is stopped or removed, the file is automatically deleted. The next time the container performs the same steps from start to end. To resolve this issue, Docker provides volumes (storage).
   ```
   docker run -it --rm -v myvol1:/myreactapp/ imageid
   ```
   (Here, `-v` means volume, `myvol1` is the volume name, and `:/myreactapp/` is the directory name. Make sure it matches the directory name mentioned in the Dockerfile.)

   **Note:** Volumes are only present locally. To see related volume commands:
   ```
   docker volume --help
   ```

**Docker External File Mount**

1. Suppose we have a file called `users.txt`, and in this file, we have 10 records. After creating an image and running it in the container, we realize we need to add more data. It's not a good practice to add data and recreate the image each time. To resolve this problem, we can mount or bind the `users.txt` file from our local machine to the container's `users.txt` file using the following command:
   ```
   docker run -v absolute_path_of_your_local_file:/myreactapp/user.txt --rm image_id
   ```
   (Here, we are mounting our local machine's `users.txt` file to the container's `users.txt` file)

**Docker .dockerignore File**

1. If we want to exclude certain folders or files from being sent in a Docker image, such as `node_modules` and `.git` folders, we can create a `.dockerignore` file. In this file, we list the folders and files that we don't want to include in the Docker image.

**Communication between Containers**

1. Suppose we have a program that fetches data from an API, web server, or a local MySQL database installed on our computer. Alternatively, we might have two containers: one for API development and another for a frontend React application. In another scenario, one container might have MySQL installed, and we need to fetch data from that container to another container where our program resides. To handle such situations, we utilize Docker's network concept.

- To install a package into our container for easy use:
  ```
  RUN composer require laravel/ui
  ```
  (This command should be included in the Dockerfile)

- To interact with a local database from within a container, use:
  ```
  host:"host.docker.internal"
  ```
  (This should be our host name)

- To obtain information about a container, including its IP network or gateway (useful when one container needs to interact with another):
  ```
  docker inspect container_name
  ```
  (This command retrieves information about our container, such as its IP address or gateway, which can then be used in other containers for communication purposes.)

**Docker Network**

1. Suppose we have two containers: one responsible for MySQL and the other for our React app. We need to connect them, but the problem arises when we have to find the IP address of the first container and replace it in the other container's host value. Additionally, we have to create an image. To overcome this hurdle, Docker provides Docker networks. We can create a network and bind both containers to this network. Then, we simply need to give the first container's name in the host value.

- To see Docker network commands:
  ```
  docker network --help
  ```

- To create a network:
  ```
  docker network create my-net
  ```
  (Here, `my-net` is your network name)

- To list networks:
  ```
  docker network ls
  ```

- To run the MySQL container and bind it to the `my-net` network:
  ```
  docker run -d --env MYSQL_ROOT_PASSWORD="root" --env MYSQL_DATABASE="userinfo" --name mysqldb --network my-net mysql
  ```

- To run the first container and bind it to the `my-net` network (ensure you replace the host name with the first container name and create a new image bound to the `my-net` network):
  ```
  docker run -it --rm --network my-net b9b6a3facc24
  ```
