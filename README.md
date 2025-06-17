# KenBen

![kenben](https://raw.githubusercontent.com/SarahZimmermann-Schmutzler/kenben_deploy/main/img_github/kenben.png)

**KenBen** is a lightweight **project management tool** based on the Kanban methodology, designed to help teams and individuals visualize workflows, organize tasks and improve productivity.

The project was created as part of my **backend training at the Developer Akademie**.

## Table of Contents

1. [Prerequisites](#prerequisites)
1. [Quickstart](#quickstart)
1. [Usage](#usage)
   * [Setup Guide](#setup-guide)
   * [Description](#description)
     * [Backend](#backend-django-and-django-rest-framework)
     * [Frontend](#frontend-angular-and-material-design-lite)

## Prerequisites

* **Angular CLI** 15.2.0, [More Information](https://github.com/angular/angular-cli)
  * **Material Design Lite**, [More Information](https://getmdl.io/)
* **Python** 3.12.2, [More Information](https://www.python.org/)
  * **Django** 5.0, [More Information](https://www.djangoproject.com/)
    * **Django REST framework** 3.14.0, [More Information](https://www.django-rest-framework.org/)
* **Docker** 24.0.7, [More Information](https://www.docker.com/)
  * **Compose** v2.32.4, [More Information](https://docs.docker.com/compose/)

## Quickstart

This section provides a **minimal setup guide**. For detailed instructions and alternative setups without GitHub Actions, see [Usage](#usage) section.  

1. [Fork](https://docs.github.com/de/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) the project to your namespace.

1. Set the required **Actions secrets and variables**
   * See the full list [here](#usage)

1. Create a **persistent volume** on your remote server

   ```bash
   docker volume create kenben-volume
   ```

1. **Manually trigger** the deployment workflow
   * * <ins>In the GitHub UI, you can find it under:</ins>
       * **Actions > Build & Deploy Kenben > Run workflow**

## Usage

### Setup Guide

**KenBen** can be run in three ways:

* [**For local development without Docker**](https://github.com/SarahZimmermann-Schmutzler/kenben_deploy/blob/main/.alternative_setups.md)
* [**Using Docker manually**](https://github.com/SarahZimmermann-Schmutzler/kenben_deploy/blob/main/.alternative_setups.md)
* **Automatically on a remote server via GitHub Actions** – follow the steps below:

1. [Fork](https://docs.github.com/de/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) the project to your namespace.

1. Set the required **Actions secrets and variables**:

   * To run the **GitHub Actions workflow** and generate the **.env file**, you must configure the following secrets and variables under:
      * **Settings > Security > Secrets and variables > Actions**

    | Key | Description |
    | --- | ----------- |
    | **Secrets for workflow** | |
    | REMOTE_HOST | IP address of remote server |
    | REMOTE_USER | Username on remote server |
    | SSH_PORT | SSH Port |
    | SSH_PRIVATE_KEY | Private SSH key of remote server |
    | DEPLOY_DIR | Path to the folder in which the project should be published |
    | **Secrets for application used in .env** | |
    | SECRET_KEY | Essential cryptographic key used by Django to protect sensitive data and provide security-critical functionality |
    | **Secrets for containerization used in .env** | |
    | DJANGO_SUPERUSER_USERNAME | Username to create a superuser for the admin panel |
    | DJANGO_SUPERUSER_EMAIL | Email address to create a superuser for the admin panel |
    | DJANGO_SUPERUSER_PASSWORD | Password to create a superuser for the admin panel |
    | **Variables for workflow** | |
    | IMAGE_OWNER | Specifies the namespace under which the Docker image will be published to the GitHub Container Registry (ghcr.io) |
    | **Variables for application used in .env** | |
    | DEBUG | Set to True to enable debug mode for local development/testing; Set to False in production environments |
    | IP_ADDRESS_VM | Server IP address, added to the ALLOWED_HOSTS list in settings.py |
    | CORS_ALLOWED_ORIGINS | List of all hosts with their portnumbers, added to settings.py |
    | **Variables for containerization used in .env** | |
    | BACKEND_EXTERNAL_PORT | External portnumber for backend container |
    | FRONTEND_EXTERNAL_PORT | External portnumber for frontend container |

1. Create a **persistent volume** on your remote server

   * To ensure your data is not lost after container restarts:
  
      ```bash
      docker volume create kenben-volume
      ```

1. **Manually trigger** the deployment workflow

   * In the `deployment.yml`, the `workflow_dispatch` trigger is enabled, so the workflow must be triggered manually:
     * * <ins>In the GitHub UI, you can find it under</ins>
       * **Actions > Build & Deploy Kenben > Run workflow**

   * <ins>Alternative</ins>: Enable **Auto-Deploy on Push** if you'd prefer automatic deployment when pushing to the main branch:
     * [Clone](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) the project to your platform:
       * <ins>Example</ins>: Clone the repo e.g. using an SSH-Key:  

          ```bash
          git clone git@github.com:Your-Name/kenben_deploy.git
          ```

       * Navigate to the **project directory**:

          ```bash
          cd kenben_deploy
          ```

     * Enable **lines 4-5** in [`deployment.yml`](https://github.com/SarahZimmermann-Schmutzler/kenben_deploy/blob/main/.github/workflows/deployment.yml)

     * **Commit and push** the change to the `main branch` - the workflow will run automatically

### Description

#### Backend (Django and Django REST framework)

This is where the core **focus of this application** lies.  
  
The **main goals** were to:

* design and implement a robust **data model using Django**
* build a custom **RESTful API**
* apply the **Django REST Framework (DRF) to handle serialization and request handling**
* create a **seamless connection** between the backend and the Angular frontend

The backend consists of **two main areas**:

* **Authentication and Authorization**
  * Handles user creation, authentication and token-based authorization

* **Workspace module**
  * Contains the main Kanban logic with the following models:
    * **Boards** – representing individual projects
    * **Tickets** – primary tasks or issues on a board
    * **Subtasks** – smaller, structured steps within a ticket

Each component is exposed through the API and supports **full CRUD operations**.

#### Frontend (Angular and Material Design Lite)

The frontend was built using **Angular** with the goal of keeping the interface simple and focused. It uses **Material Design Lite (MDL)** for styling, providing a clean and lightweight UI without relying on a predefined mockup.  
  
**Key features** of the frontend include:

* **Authentication**:
  * **Login page** (username & password)
  ![login](https://raw.githubusercontent.com/SarahZimmermann-Schmutzler/kenben_deploy/main/img_github/kenben.png)
  * **Register page** (username, email, password)
  ![register](https://raw.githubusercontent.com/SarahZimmermann-Schmutzler/kenben_deploy/main/img_github/register.png)

* **Workspace view**:
  * Displays all **existing boards**
  * Allows **creation of new boards**
  ![worspace](https://raw.githubusercontent.com/SarahZimmermann-Schmutzler/kenben_deploy/main/img_github/workspace.png)

* **Board view**:
  * Shows **columns** for task status (To Do, In Progress, Awaiting Feedback and Done)
  * **Tickets** are organized within these columns and can be moved via **drag-and-drop**
  ![board](https://raw.githubusercontent.com/SarahZimmermann-Schmutzler/kenben_deploy/main/img_github/board.png)
  * New tickets can be **created** and existing ones **edited** (including adding, updating or deleting subtasks)
  ![ticket](https://raw.githubusercontent.com/SarahZimmermann-Schmutzler/kenben_deploy/main/img_github/ticket.png)
  ![edit](https://raw.githubusercontent.com/SarahZimmermann-Schmutzler/kenben_deploy/main/img_github/edit.png)

The frontend communicates with the Django-based API to **fetch and update all data in real time**.
