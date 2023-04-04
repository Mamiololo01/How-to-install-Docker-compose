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
