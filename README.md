# Docker-Project
Docker setup documentation
Setting Up a WordPress Site with Docker
This guide walks you through the process of setting up a WordPress site using Docker.

Prerequisites
Docker installed and running on your machine.
Basic knowledge of Docker and the command line.
Docker Compose installed.
Steps
1. Create a Project Directory

mkdir wordpress-docker
cd wordpress-docker
3. Create a docker-compose.yml File
Create a docker-compose.yml file inside your project directory and add the following content:

yaml
Copy code
version: '3.8'

services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress-container
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wp_user
      WORDPRESS_DB_PASSWORD: wp_password
      WORDPRESS_DB_NAME: wp_database
    volumes:
      - wordpress_data:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:5.7
    container_name: wordpress-db
    environment:
      MYSQL_ROOT_PASSWORD: root_password
      MYSQL_DATABASE: wp_database
      MYSQL_USER: wp_user
      MYSQL_PASSWORD: wp_password
    volumes:
      - db_data:/var/lib/mysql

volumes:
  wordpress_data:
  db_data:
3. Start the Containers
Run the following command in the project directory to start the WordPress and MySQL containers:

docker-compose up -d
4. Access WordPress
Open a browser and go to http://localhost:8000. You’ll see the WordPress setup page.

5. Set Up WordPress
Choose your preferred language.
Enter the database details as specified in docker-compose.yml:
Database Name: wp_database
Username: wp_user
Password: wp_password
Database Host: db
Complete the setup and log in to your WordPress site.
6. Managing the Environment
Stop Containers: docker-compose down
Restart Containers: docker-compose up -d
View Logs: docker-compose logs
7. Customization
You can:

Update the docker-compose.yml to use custom themes or plugins by mounting additional volumes.
Create backups of the WordPress database by accessing the MySQL container.
8. Cleanup
To remove the setup entirely, including the data, run:

docker-compose down --volumes
