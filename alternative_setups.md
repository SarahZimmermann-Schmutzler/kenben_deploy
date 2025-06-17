# KenBen - Alternative Setup Guides

If you don't want to work with Github Actions, there are **other ways to use KenBen**, either locally or with Docker.

## Table of Contents

1. [Run KenBen locally without Docker](#run-kenben-locally-without-docker)
1. [Run KenBen with Docker manually](#run-kenben-with-docker-manually)

## Run KenBen locally without Docker

1. [Clone](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) the project to your platform:
    * <ins>Example</ins>: Clone the repo e.g. using an SSH-Key:  

        ```bash
        git clone git@github.com:SarahZimmermann-Schmutzler/kenben_deploy.git
        ```

    * Navigate to the **project directory**:

        ```bash
        cd kenben_deploy
        ```

1. Navigate into the **backend directory** and create an `.env` file with the following variables:

    ```bash
    cd kenben
    nano .env
    ```

    | Variable | Description | Default Value |
    | -------- | ----------- | ------------- |
    | DEBUG | Set to True to enable debug mode for local development/testing; Set to False in production environments | True |
    | SECRET_KEY | Essential cryptographic key used by Django to protect sensitive data and provide security-critical functionality | [create](https://stackoverflow.com/questions/41298963/is-there-a-function-for-generating-settings-secret-key-in-django) |

1. Create a **virtual environment** and **install Python packages**:

    ```bash
    python -m venv env
    source venv/bin/activate
    pip install -r requirements.txt
    ```

1. **Start the backend**:

    ```bash
    python manage.py runserver
    ```

1. In a **second terminal**, navigate into the **frontend directory** and **install the frontend dependencies**:

    ```bash
    cd ..
    cd kenben_frontend
    npm install
    ```

1. **Start the frontend**:

    ```bash
    ng serve
    ```

## Run KenBen with Docker manually

1. [Clone](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) the project to your platform:
    * <ins>Example</ins>: Clone the repo e.g. using an SSH-Key:  

        ```bash
        git clone git@github.com:SarahZimmermann-Schmutzler/kenben_deploy.git
        ```

    * Navigate to the **project directory**:

        ```bash
        cd kenben_deploy
        ```

1. Init and update the **submodules**:

    ```bash
    git submodule init
    git submodule update
    ```

1. Configure the **environment variables**:
    * Copy the content of the [`example.env`](https://github.com/SarahZimmermann-Schmutzler/kenben_deploy/blob/main/example.env) file into an .env file.

    | Variable | Description | Default Value |
    | -------- | ----------- | ------------- |
    | **For backend application** | | |
    | DEBUG | Set to True to enable debug mode for local development/testing; Set to False in production environments | True |
    | SECRET_KEY | Essential cryptographic key used by Django to protect sensitive data and provide security-critical functionality | [create](https://stackoverflow.com/questions/41298963/is-there-a-function-for-generating-settings-secret-key-in-django) |
    | IP_ADDRESS_VM | Server IP address, added to the ALLOWED_HOSTS list in settings.py | 127.0.0.1 |
    | CORS_ALLOWED_ORIGINS | List of all hosts with their portnumbers, added to settings.py | http://localhost:4200 |
    | **For containerization** | | |
    | BACKEND_EXTERNAL_PORT | External portnumber for backend container | 8000 |
    | FRONTEND_EXTERNAL_PORT | External portnumber for frontend container | 8080 |
    | DJANGO_SUPERUSER_USERNAME | Username to create a superuser for the admin panel | admin |
    | DJANGO_SUPERUSER_EMAIL | Email address to create a superuser for the admin panel | admin@example.com |
    | DJANGO_SUPERUSER_PASSWORD | Password to create a superuser for the admin panel | changeme123 |

1. **Build and start the containers** in the background (detached mode):

    ```bash
    docker compose up --build -d
    ```

1. Check whether the **containers are running** correctly:

    ```bash
    docker ps -a
    ```
