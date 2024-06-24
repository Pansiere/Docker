# Step-by-Step Guide to Setup MySQL User for PhpMyAdmin Access in Docker

## 1. Create a .env File

Create a **.env** file in your project directory and add the MySQL root password. Replace your_root_password with your desired MySQL root password.

1. ```BASH
      nano .env
   ```

   paste into your **.env** file:

2. ```BASH
   MYSQL_ROOT_PASSWORD=your_root_password
   ```

## 2. Make a docker compose file: docker-compose.yaml

1. Create the docker compose file:

```YAML
version: "3.9"
services:
db:
  image: mysql/mysql-server:latest
  container_name: mysql
  restart: always
  environment:
    - MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
  ports:
    - "3306:3306"
  volumes:
    - mysql-volume:/var/lib/mysql
phpmyadmin:
  image: phpmyadmin/phpmyadmin:latest
  container_name: my-phpmyadmin
  restart: always
  environment:
    - PMA_HOST=db
    - PMA_USER=yourusername
    - PMA_PASSWORD=${MYSQL_ROOT_PASSWORD}
  ports:
    - "8080:80"
volumes:
mysql-volume:
  driver: local
```

2. Run the contaienr

```BASH
docker compose up -d
```

## 2. Login to MySQL Docker Container

Use Docker to access the MySQL command-line interface.

```BASH
docker exec -it <container_name_mysql> mysql -u root -p
```

Replace <container_name_mysql> with the actual name of your MySQL Docker container. It will prompt for the MySQL root password (MYSQL_ROOT_PASSWORD from your .env file).

Example:

```BASH
docker exec -it mysql-container mysql -u root -p
```

## 3. Create a PhpMyAdmin User

Inside the MySQL command-line interface, execute the following commands to create a user (**yourusername** in this example) that PhpMyAdmin can use to connect.

```sql
CREATE USER 'yourusername'@'172.21.0.3' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON _._ TO 'yourusername'@'172.21.0.3' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

- **'yourusername'@'172.21.0.3'**: Replace 'yourusername' with your desired username and 172.21.0.3 with the IP address where PhpMyAdmin is hosted. This allows MySQL connections from PhpMyAdmin hosted on that IP address.
- **'password'**: Replace with the same password used inside the **.env** file.

## 4. Login to PhpMyAdmin:

Access PhpMyAdmin via the browser using the URL or IP address where PhpMyAdmin is hosted (172.21.0.3 in this example).
URL: <http://172.21.0.3/phpmyadmin/>
Login with the MySQL user (yourusername) and the password (password) you set earlier.  
Or acess the IP adress of the container's host: **container-host-IP:8080**

## Additional Notes:

- Ensure your Docker networking setup (172.21.0.3 in this case) matches where PhpMyAdmin is accessible.
- Adjust IP addresses (172.21.0.3), usernames (yourusername), and passwords (password) according to your actual configuration.
- Always use strong, secure passwords and keep your .env and configuration files safe.

Following these steps should allow you to set up a MySQL user that PhpMyAdmin can use to connect to your Dockerized MySQL database.
