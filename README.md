# How-to-install-Docker-compose
Step by step guide to install Docker compose

Introduction
Docker simplifies the process of managing application processes in containers. While containers are similar to virtual machines in certain ways, they are more lightweight and resource-friendly. This allows developers to break down an application environment into multiple isolated services.

For applications depending on several services, orchestrating all the containers to start up, communicate, and shut down together can quickly become unwieldy. Docker Compose is a tool that allows you to run multi-container application environments based on definitions set in a YAML file. It uses service definitions to build fully customizable environments with multiple containers that can share networks and data volumes.

In this guide, you’ll demonstrate how to install Docker Compose on an Ubuntu 20.04 server and how to get started using this tool.

Prerequisites

To follow this article, you will need:

Access to an Ubuntu 20.04 local machine or development server as a non-root user with sudo privileges. If you’re using a remote server, it’s advisable to have an active firewall installed. To set these up, please refer to our Initial Server Setup Guide for Ubuntu 20.04.

Docker installed on your server or local machine, following Steps 1 and 2 of How To Install and Use Docker on Ubuntu 20.04.

Step 1 — Installing Docker Compose
To make sure you obtain the most updated stable version of Docker Compose, you’ll download this software from its official Github repository.

First, confirm the latest version available in their releases page. At the time of this writing, the most current stable version is 1.29.2.

The following command will download the 1.29.2 release and save the executable file at /usr/local/bin/docker-compose, which will make this software globally accessible as docker-compose:

<img width="899" alt="Screenshot 2023-04-04 at 22 56 52" src="https://user-images.githubusercontent.com/67044030/229935446-0c1f0b2d-279e-4a26-a7f5-8129d75a8845.png">

Next, set the correct permissions so that the docker-compose command is executable:

sudo chmod +x /usr/local/bin/docker-compose

<img width="829" alt="Screenshot 2023-04-04 at 22 57 14" src="https://user-images.githubusercontent.com/67044030/229935716-56bed5b4-ccec-4367-be6e-8a30ee5073c6.png">

To verify that the installation was successful, you can run:

docker-compose --version

<img width="724" alt="Screenshot 2023-04-04 at 22 57 38" src="https://user-images.githubusercontent.com/67044030/229935930-f34c9415-93f4-4a61-bc90-41a9a7d53341.png">


Docker Compose is now successfully installed on your system. In the next section, you’ll see how to set up a docker-compose.yml file and get a containerized environment up and running with this tool.

Step 2 — Setting Up a docker-compose.yml File

To demonstrate how to set up a docker-compose.yml file and work with Docker Compose, you’ll create a web server environment using the official Nginx image from Docker Hub, the public Docker registry. This containerized environment will serve a single static HTML file.

Start off by creating a new directory in your home folder, and then moving into it:

mkdir ~/compose-demo

cd ~/compose-demo

<img width="631" alt="Screenshot 2023-04-04 at 22 58 57" src="https://user-images.githubusercontent.com/67044030/229936216-bb26b3dd-121e-4648-8fd2-94f28ea9369d.png">

In this directory, set up an application folder to serve as the document root for your Nginx environment:

mkdir app
Using your preferred text editor, create a new index.html file within the app folder:

nano app/index.html



Save and close the file when you’re done. If you are using nano, you can do that by typing CTRL+X, then Y and ENTER to confirm.

Next, create the docker-compose.yml file:

nano docker-compose.yml
Insert the following content in your docker-compose.yml file:


The docker-compose.yml file typically starts off with the version definition. This will tell Docker Compose which configuration version you’re using.

You then have the services block, where you set up the services that are part of this environment. In your case, you have a single service called web. This service uses the nginx:alpine image and sets up a port redirection with the ports directive. All requests on port 8000 of the host machine (the system from where you’re running Docker Compose) will be redirected to the web container on port 80, where Nginx will be running.

The volumes directive will create a shared volume between the host machine and the container. This will share the local app folder with the container, and the volume will be located at /usr/share/nginx/html inside the container, which will then overwrite the default document root for Nginx.

Save and close the file.

You have set up a demo page and a docker-compose.yml file to create a containerized web server environment that will serve it. In the next step, you’ll bring this environment up with Docker Compose.

Step 3 — Running Docker Compose

With the docker-compose.yml file in place, you can now execute Docker Compose to bring your environment up. The following command will download the necessary Docker images, create a container for the web service, and run the containerized environment in background mode:

docker-compose up -d
Docker Compose will first look for the defined image on your local system, and if it can’t locate the image it will download the image from Docker Hub. You’ll see output like this:


Note: If you run into a permission error regarding the Docker socket, this means you skipped Step 2 of How To Install and Use Docker on Ubuntu 20.04. Going back and completing that step will enable permissions to run docker commands without sudo.

Your environment is now up and running in the background. To verify that the container is active, you can run:

docker-compose ps

This command will show you information about the running containers and their state, as well as any port redirections currently in place:


You can now access the demo application by pointing your browser to either localhost:8000 if you are running this demo on your local machine, or your_server_domain_or_IP:8000 if you are running this demo on a remote server.

You’ll see a page like this:


