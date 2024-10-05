# Client Server Architecture using MySQL Database Management System 

Client-server architecture is a model in which two or more machines communicate over a network, each with distinct roles. The client, typically a web browser or an application, initiates requests for resources, while the server, responsible for processing these requests, responds accordingly. In the context of a MySQL database, the client application sends queries—such as retrieving, updating, or deleting data—to the MySQL server. The server processes these SQL commands, interacting with the database to return the requested information or execute changes. This architecture enables a separation of concerns, with the client handling user interactions and interface rendering, while the server manages data persistence, security, and logic processing. Data exchange occurs over standard protocols like HTTP or TCP/IP, and the connection is often secured with encryption (SSL/TLS) to ensure data integrity. This model supports scalability, enabling multiple clients to interact with a central database server concurrently.
To demmonstarted a basic client-server using MySQL RDBS, follow the bellow instructions

- Create and configure two EC2 Instances of t2.micro type and Ubuntu 24.04 LTS (HVM) and launched in the us-east-1 region using the AWS console.

Server A name -  ``mysql-server``

Server B name -  ``mysql-client``

![WhatsApp Image 2024-10-05 at 16 19 10_0cbb8da8](https://github.com/user-attachments/assets/399f188b-e56d-409c-85a1-ea30f6812e0a)

- On mysql server install MySQL server software

```bash
sudo apt-get update
sudo apt-get install mysql-server
```

![WhatsApp Image 2024-10-01 at 20 52 00_53172131](https://github.com/user-attachments/assets/2863bed1-39b0-431e-a040-92ac438ade1e)

- On mysql client Linux Server install MySQL client software.

```bash
sudo apt-get update
sudo apt-get install mysql-client
```

![WhatsApp Image 2024-10-05 at 11 56 37_ffae4c18](https://github.com/user-attachments/assets/9326765b-de35-41fc-b290-10def4a2dffc)

- Enable mysql servers

```bash
sudo systemctl enable mysql
```

![WhatsApp Image 2024-10-05 at 12 00 31_c7bd5787](https://github.com/user-attachments/assets/fcd478ba-40a4-4214-a9cb-e4348f2b0371)

- On mysql server, Edit the mysql configuration file to allow remote connections; replace 127.0.0.1 to 0.0.0.0

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

 ![WhatsApp Image 2024-10-05 at 12 08 55_d075e39d](https://github.com/user-attachments/assets/ece75bce-d65e-4c8c-a5e5-b2aeef6b430d)

- To remotely connect from a MySQL client Linux server to a MySQL database engine without using SSH,Create a remote user on the MySQL server: On the server hosting the database, use the MySQL command-line tool to create a user with necessary privileges, allowing the client to securely access the database. This ensures the user has the required permissions to connect remotely from the client server to the MySQL server's database.

```bash
mysql -u root -p
```
- Create a new user: To create a new user with remote access privileges, run the following SQL command:

```bash 
CREATE USER 'remote_user'@'client_ip' IDENTIFIED BY 'strong_password';
```

- Grant privileges to the remote user: To grant privileges to the remote user, run the following SQL command:

```bash
GRANT <permissions> ON <database>.* TO 'remote_user'@'client_ip' WITH GRANT OPTION;
```

- Flush privileges: After creating the user and granting privileges, flush the privileges to ensure the changes take effect:

```bash
FLUSH PRIVILEGES;
```

![WhatsApp Image 2024-10-05 at 16 35 38_68c06b44](https://github.com/user-attachments/assets/c3a9843a-e9bc-4587-b0ae-6241bf721488)

- Exit the MySQL prompt: Type exit to exit the MySQL prompt.



- Connect from the MySQL Client: On the Linux server with the MySQL client, use the mysql utility to connect remotely to the MySQL server database engine. Use the appropriate connection parameters as follows:

```bash
 mysql -h <remote_mysql_server_ip> -u <username> -p
```
- Check that you have successfully connected to a remote MySQL server and can perform SQL queries:

```bash
SHOW DATABASES;
```

![WhatsApp Image 2024-10-05 at 12 22 26_e6b482db](https://github.com/user-attachments/assets/b1ff1f3a-5799-4751-8333-ec1d71a4eb89)

  - To ensure functionality, let's utilize the MySQL client to create and drop databases and tables, and to insert and select records from them.Create a Database: To create a new database. This will create a new database named "Bloomdb". You can use the following command:

```bash
CREATE DATABASE BloomDB;
```
Use the Database: After creating the database, you need to switch to it using the USE command:
![WhatsApp Image 2024-10-05 at 16 52 15_99d347b5](https://github.com/user-attachments/assets/3f6601a5-297c-4a6a-b7c6-c322b6623bc4)


```bash
USE BloomDB;
```

- Create a Table: Let's create a simple table called "users" with two columns: "id" and "name".
```bash
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50)
);
```
- Insert Records: You can insert records into the "users" table using the INSERT INTO command:
 
```bash
INSERT INTO users (name) VALUES ('EMMA'), ('FORTIS'), ('PONMILE'), ('DARE');
```
- Drop Table and Database (Optional): If you want to clean up, you can drop the table and the database:
 
 ```bash
DROP DATABASE Bloomdb;
```
- Exit MySQL: Finally, when you're finished, you can exit the MySQL command-line interface by typing:
exit

![WhatsApp Image 2024-10-05 at 16 59 28_68c78b9f](https://github.com/user-attachments/assets/75c43ede-a7ca-4fa3-b0c2-0560aac23ba4)

### At this point, this project is successfully complete. This deployment is a fully functional MySQL Client-Server set up.
