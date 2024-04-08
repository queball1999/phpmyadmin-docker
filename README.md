# phpMyAdmin & MySQL Docker Setup

This repository provides a quick, one-click solution to set up phpMyAdmin and MySQL using Docker and Docker Compose. With just a few commands, you can have a running instance of MySQL and phpMyAdmin, accessible via ports 3306 and 80 respectively.

## Prerequisites

Before you begin, ensure you have Docker and Docker Compose installed on your system. If not, follow the installation instructions for your operating system:

### Installing Docker

- **For Windows and macOS:**
  - Download and install Docker Desktop from [Docker Hub](https://hub.docker.com/?overlay=onboarding).
- **For Linux:**
  - Use your distribution's package manager to install Docker. For example, on Ubuntu, you can run:
    ```bash
    sudo apt update
    sudo apt install docker.io
    ```
  - To install Docker on other Linux distributions, refer to the official Docker documentation.

### Installing Docker Compose

- Docker Desktop for Windows and macOS includes Docker Compose.
- For Linux, after installing Docker, run:
  ```bash
  sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  ```
## Setting Up

### Clone the Repository:
Begin by cloning this repository to your local machine using:

```bash
git clone <REPOSITORY_URL>
cd <REPOSITORY_NAME>
```
After cloning, you can directly proceed to "Starting the Containers" section as the docker-compose.yaml file is already set up for you in the repository.

### Create a Directory and Configuration File
If you prefer to start from scratch rather than cloning, follow these steps:

- **Create a new directory for your project and navigate into it:**
   ```bash
   mkdir my-phpmyadmin-setup
   cd my-phpmyadmin-setup
   ```
- Create a docker-compose.yaml file with the following content:
   ```bash
   version: '3.1'

   services:
     db:
       image: mysql
       command: --default-authentication-plugin=mysql_native_password
       restart: always
       environment:
         MYSQL_ROOT_PASSWORD: [root_passowrd]
       ports:
         - "3306:3306"

     phpmyadmin:
       image: phpmyadmin/phpmyadmin
       restart: always
       environment:
         PMA_HOST: db
         MYSQL_ROOT_PASSWORD: [root_passowrd]
       ports:
         - "80:80"
       depends_on:
         - db
   ```

### Starting the Containers:
- Run the following command in the directory where your docker-compose.yaml is located:
```bash
docker-compose up -d
```
- This command will download the necessary Docker images and start the containers in detached mode.

### Stopping the Containers
To stop the running containers, use the following command in the same directory as your docker-compose.yaml:

```bash
docker-compose down
```

## Usage
After starting the containers, you can access:

- MySQL: Through port 3306 on your host machine.
- phpMyAdmin: Through port 80 on your host machine by navigating to http://localhost in your web browser.

![image](https://github.com/queball1999/phpmyadmin-docker/assets/57122349/90c13dd9-d936-45ea-b927-6130b6da5c55)


## Contributing
Contributions are welcome! If you have improvements or bug fixes, please feel free to fork the repository and submit a pull request.
