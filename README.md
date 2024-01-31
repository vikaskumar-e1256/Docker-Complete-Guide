# Docker-Complete-Guide

Certainly! Here is the content converted into a Markdown (.md) file format:

```markdown
# Docker File Creation Commands

1. **Create Dockerfile**: 
   - Create a Dockerfile without any extension.
   
2. **Check Node Module Folder**: 
   - Ensure the absence of the `node_module` folder.

3. **Install NodeJS**: 
   - Include instructions in the Dockerfile for NodeJS installation.
   ```Dockerfile
   FROM node
   ```

4. **Specify NodeJS Version**:
   - Add a specific NodeJS version if required.
   ```Dockerfile
   FROM node:20
   ```

5. **Set Working Directory**:
   - Establish a working directory for running the React app.
   ```Dockerfile
   WORKDIR /myreactapp
   ```

6. **Copy Work to Container**: 
   - Copy all work into the `myreactapp` folder.
   ```Dockerfile
   COPY . .
   ```

7. **Install Packages**: 
   - Run `npm install` for package installation.
   ```Dockerfile
   RUN npm install
   ```

8. **Expose Port**:
   - Specify a different port if necessary.
   ```Dockerfile
   EXPOSE 3001
   ```

9. **Run Docker Image**:
   - Command to run the Docker image.
   ```Dockerfile
   CMD [ "npm", "run", "dev" ]
   ```

# Make a Docker Image Command

1. **Build Docker Image**:
   - Navigate to the project directory and execute the following command in the terminal:
   ```bash
   docker build .
   ```

2. **Tag Docker Image**:
   - Tag the Docker image for better identification.
   ```bash
   docker build -t myfirstimage:01 .
   ```

3. **Remove Image**:
   - Delete an image using:
   ```bash
   docker rmi myfirstimage:01
   ```

# Basic Commands of Docker

1. **List Images**:
   - View all images with:
   ```bash
   docker image ls
   ```

2. **Create Container**:
   - Run a container using its image ID.
   ```bash
   docker run image_id
   ```

3. **Check Containers**:
   - View running containers:
   ```bash
   docker ps
   ```
   - To see all containers (running or stopped):
   ```bash
   docker ps -a
   ```

4. **Remove Containers**:
   - Delete multiple containers by specifying their names:
   ```bash
   docker rm container_name_1 container_name_2 container_name_3
   ```

5. **Stop Container**:
   - Terminate a container:
   ```bash
   docker stop container_name
   ```

6. **Bind Ports**:
   - Make containers accessible via the browser:
   ```bash
   docker run -p 5173:5173 ff2ce433d9b1
   ```

7. **Detach Mode**:
   - Run containers in the background:
   ```bash
   docker run -d -p 5173:5173 ff2ce433d9b1
   ```

8. **Auto Removal**:
   - Automatically remove containers upon stopping:
   ```bash
   docker run -d --rm -p 3002:5173 ff2ce433d9b1
   ```

9. **Assign Container Name**:
   - Give a custom name to the container:
   ```bash
   docker run -d --rm --name "reactappcontainer" -p 3002:5173 ff2ce433d9b1
   ```

# Running Multiple Containers by a Single Image

To run multiple containers from a single image, assign different ports:
```bash
docker run -d -p 3002:5173 ff2ce433d9b1
docker run -d -p 3001:5173 ff2ce433d9b1
```
```
