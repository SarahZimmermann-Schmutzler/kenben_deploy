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
