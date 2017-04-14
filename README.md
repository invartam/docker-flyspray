# Presentation
This image provide the flyspray bugtracker packed with nginx and php-fpm 7.0 on Alpine Linux.

# How to use it
Before using this flyspray image, you should have a MySQLi compatible server fully functionnal.
Here a docker-compose example to run this flyspray image with MariaDB :

    version: "2"
    services:
    mysql:
        image: mariadb
        container_name: mysql
        environment:
        - MYSQL_ROOT_PASSWORD=test
        - MYSQL_DATABASE=flyspray
        expose:
        - 3306

    phpmyadmin:
        image: phpmyadmin/phpmyadmin
        container_name: phpmyadmin
        depends_on:
        - mysql
        environment:
        - PMA_HOST=mysql
        - PMA_USER=root
        - PMA_PASSWORD=test
        ports:
        - "8080:80"

    flyspray:
        image: invartam/docker-flyspray
        container_name: flyspray
        depends_on:
        - mysql
        ports:
        - "80:80"
