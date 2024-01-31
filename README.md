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
