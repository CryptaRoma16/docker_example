# Docker Example :whale:
- Localhost server using docker and VS
- A simple example of running a localhost server on port 9000 using Docker.
- Here's the Step-by-step guide:

1. Install Docker for Windows Desktop https://www.docker.com/
   - After installation: Open Command Prompt type: ```cd \ ```, ```wsl --install```, ```wsl --update```
   - Once the Docker engine running...
2. Install Visual Studio Code https://code.visualstudio.com/download
3. On VSC, go to extensions - install Docker and Express
4. Create a folder on your C drive - :open_file_folder: ```C:\Docker Example```
5. Then open the Docker Example folder from VSC
    #### List of files inside the Docker folder to create:
          server.js, Dockerfile, and package.json
   ![Docker Example Folder](https://github.com/CryptaRoma16/docker_example/blob/main/img/folder.png)
   
7. Create a simple server file (server.js)

```js
const express = require("express");
const app = express();
const PORT = 9000;

app.get("/",(req, res) => {
    res.send("<h1>Hello! Port 9000 from Docker,<br> Follow me on my Github <a href='https://github.com/CryptaRoma16'>CrytaRoma16</a></h1>");
});

app.listen(PORT, "0.0.0.0",() => {
    console.log(`Server running at http://localhost:${PORT}`);
});

```
7. Create a Dockerfile
   
```js
FROM node:18

# Create app directory
WORKDIR /usr/src/app

# Copy package.json (if you have one) or skip if not
COPY package*.json ./

#Install dependencies
RUN npm install

# Copy the rest of the code
COPY . .

# Expose port 9000
EXPOSE 9000

# Start the server
CMD ["node","server.js"]
```
8. Try to build and run, Open in Integrated Terminal inside on Docker Example folder. (Right-Click and select terminal)<br>
   Type:<br>
   ```docker build -t my-app .```<br>
   ```docker run -p 9000:9000 my-app```<br>

   Note: *my-app* is your tag name for your server to build and run it.<br>

   If there's an error: ```Error: cannot find module 'express'```

Fix 1: Add express properly
If you want to use Express, you must have a package.json and install dependencies inside the container.

9. Create a package.json
```
{
    "name":"my-node-server",
    "version":"1.0.0",
    "main":"server.js",
    "dependencies": {
        "express":"^4.18.2"
    }
}
```
10. Now Try to build and run again.
   Type:<br>
    ### Build
          ```docker build -t mynewapp .```
   ![Docker build image should look like on the terminal](https://github.com/CryptaRoma16/docker_example/blob/main/img/build.png)
   

   ### Run
      ```docker run -p 9000:9000 mynewapp```
   ![Docker run image should look like on the terminal](https://github.com/CryptaRoma16/docker_example/blob/main/img/run.png)

   Go to your browser type this url:
   ### Webserver (localhost)
      ```http://localhost:9000```
   ![The output](https://github.com/CryptaRoma16/docker_example/blob/main/img/localhost.png)


---
