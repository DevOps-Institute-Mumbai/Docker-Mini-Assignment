### Step-by-Step Solution for Creating a Dockerized Node.js Application

#### **Prerequisites**
Before starting, ensure the following prerequisites are met:
1. **Docker Installed**: Ensure Docker is installed on your system. You can find installation guides for different platforms on the Docker website.
2. **Basic Command-Line Knowledge**: Familiarity with basic command-line operations will be helpful since Docker is typically managed through the terminal.

---

#### **Step 1: Create a Simple Node.js Application**

1. **Create a Directory**:
   - Open your terminal and create a directory for your project.
     ```bash
     mkdir my-docker-app
     ```
   - Navigate into the project directory:
     ```bash
     cd my-docker-app
     ```

2. **Create `app.js`**:
   - Inside your project directory, create a file called `app.js` and add the following content:
     ```javascript
     const http = require('http');

     const server = http.createServer((req, res) => {
       res.writeHead(200, { 'Content-Type': 'text/plain' });
       res.end('Hello, Docker World!\n');
     });

     const port = process.env.PORT || 3000;
     server.listen(port, () => {
       console.log(`Server running on http://localhost:${port}`);
     });
     ```

   This is a simple Node.js application that sets up a web server and responds with "Hello, Docker World!" when accessed.

---

#### **Step 2: Create a Dockerfile**

1. **Create the Dockerfile**:
   - In your project directory, create a file named `Dockerfile` (no extension).
   - Add the following content to the `Dockerfile`:
     ```Dockerfile
     # Use the official Node.js image from the Docker Hub
     FROM node:14

     # Set the working directory in the container
     WORKDIR /usr/src/app

     # Copy package.json and package-lock.json to the container
     COPY package*.json ./

     # Install application dependencies
     RUN npm install

     # Copy the rest of the application source code to the container
     COPY . .

     # Expose the port your application will run on
     EXPOSE 3000

     # Define the command to run your application
     CMD ["node", "app.js"]
     ```

   The `Dockerfile` specifies:
   - The base image (`node:14`) from Docker Hub.
   - The working directory in the container.
   - Copying necessary files (`package.json`, `app.js`) and installing dependencies.
   - Exposing port 3000 for the application.
   - The command to run the Node.js application.

---

#### **Step 3: Build the Docker Image**

1. **Build the Image**:
   - In your terminal, make sure you're inside the project directory.
   - Run the following command to build the Docker image:
     ```bash
     docker build -t my-docker-app .
     ```
   - The `-t my-docker-app` flag tags the image with the name "my-docker-app".

---

#### **Step 4: Run the Docker Container**

1. **Run the Container**:
   - Now that your Docker image is built, run a Docker container from the image with this command:
     ```bash
     docker run -p 3000:3000 my-docker-app
     ```
   - This command maps port 3000 in the container to port 3000 on your host machine, allowing you to access the application via your web browser.

---

#### **Step 5: Access Your Application**

1. **Open a Web Browser**:
   - In your browser, navigate to `http://localhost:3000`.
   - You should see "Hello, Docker World!" displayed, confirming that the Dockerized application is running successfully.

---

#### **Conclusion**

Congratulations! You have successfully Dockerized a simple Node.js application. The steps you have completed include:
- Setting up a Node.js application.
- Creating a Dockerfile to package the application into a Docker image.
- Building and running a Docker container to host your application.

---
Enjoy Learning With us Folks !
