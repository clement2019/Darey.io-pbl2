      PROJECT 2: LEMP STACK IMPLEMENTATION
I started this project by first creating a lemp-stack web server in Aws in my availability zone eu-west 2a,
configured the security group with the necessary configuration settings 
SSH on port:22 and HTTP on port :80 thereby creating the necessity FIREWALL.
 I created my private key to be able to connect to my EC2 instance and with the help of the
 key i was able to use (SSH client) connection to connect to my instance using Gitbash installed on my machine
 
 ![image](https://user-images.githubusercontent.com/55473846/138353764-08acda5b-86bb-4728-a4f5-fcc3d7b9df7f.png)
 
 The above comes up when after I ran my Aws  Ec2 instance using SSh client connection with GItbash

INSTALLING THE NGINX WEB SERVER

updated my machine by running

sudo apt update
The result of the update as shown below

![image](https://user-images.githubusercontent.com/55473846/138353932-ba9ff7ea-68d0-441b-9c47-80dd5b49ddbf.png)

Next i installed Ngnix webserver by running the command below

sudo apt install nginx

![image](https://user-images.githubusercontent.com/55473846/138354082-f6dfd165-55e6-439e-a9c9-6d216581dfa9.png)

I latter confirmed the nginx webserver is running by running this command

$ sudo systemctl status nginx

As shown below the webserver is running and its shown below

![image](https://user-images.githubusercontent.com/55473846/138355709-a2fbc17c-c4cd-4fe9-bbdc-ba3befec6c73.png)

I can access traffic on port: 80 already configured while TCP port:22 is already configured and open on Ec2 as well in security group. Although it is not advisable to open all port to traffic in production mode but its because this is a test project so for now is allowed. The server is running, and it can be access locally on 0.0.0.0/0 means that any ip address can access the webserver for now.
![image](https://user-images.githubusercontent.com/55473846/138355841-3605e7e6-20a6-403c-8cc6-06d0a069db13.png)

CHECKING IF WEBSERVER IS WELL CONFIGURED

I checked to see if the webserver is well configured by checking with default Nginx webserver page as shown below

![image](https://user-images.githubusercontent.com/55473846/138356077-f1fba1e1-4b0c-4b2d-a3e7-da0278c78f3b.png)

I equally checked with the aws ec2 instance public ip address 

http://ec2-18-130-125-19.eu-west-2.compute.amazonaws.com/ 

to view the Nginx webserver page as shown below and it works

![image](https://user-images.githubusercontent.com/55473846/138356243-df2e6a5b-601b-4247-9f5d-e6cd7dba6b8c.png)

INSTALLING MYSQL

Now I have my Ngnix web server up and running, I now need to install a Database Management System (DBMS) to be able to store and manage data for my site in a relational database. MySQL is a popular relational database management system used within PHP environments; this I will use in my project.
I ran this command 
$ sudo apt install mysql-server

![image](https://user-images.githubusercontent.com/55473846/138356868-81ef22b3-ff08-4a01-aed5-69adb5f98073.png)

I ran the following command to secure mysql and remove some default settings

$ sudo mysql_secure_installation

![image](https://user-images.githubusercontent.com/55473846/138357007-7e2a401f-ebbe-4062-af5e-3236e75d033d.png)

I ran this command to be able to access mysql
$sudo mysql

![image](https://user-images.githubusercontent.com/55473846/138357199-4e15f096-bff2-43af-bec7-9bee1b2865f1.png)


INSTALLING PHP

sudo apt install php-fpm php-mysql

![image](https://user-images.githubusercontent.com/55473846/138362738-704794f8-bf35-482a-bc7c-7b3fcd17ba67.png)

CONFIGURING NGINX TO USE PHP PROCESSOR
I now have my PHP components installed. Next, i will configure Nginx to use them.
When using the Nginx web server, we can create server blocks (like virtual hosts in Apache) to encapsulate configuration details and host more than one domain on a single server. In this guide, we will use projectLEMP as an example domain name.
On Ubuntu 20.04, Nginx has one server block enabled by default and is configured to serve documents out of a directory at /var/www/html. While this works well for a single site, it can become difficult to manage if am hosting multiple sites. Instead of modifying /var/www/html, i createed a directory structure within /var/www for the  projectLEMP  website, leaving /var/www/html in place as the default directory to be served if a client request does not match any other sites.

I created the root web directory for domain as follows:

sudo mkdir /var/www/projectLEMP

I now assign ownership to this user as follows using the following command
sudo chown -R $USER:$USER /var/www/projectLEMP

I then opened a new configuration file in Nginx’s sites-available directory using my preferred command-line editor. Here, i used nano:
sudo nano /etc/nginx/sites-available/projectLEMP

![image](https://user-images.githubusercontent.com/55473846/138363007-5eda0516-d453-4941-84d5-962eaaea556c.png)

Activate my configuration by linking to the config file from Nginx’s sites-enabled directory:
sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/

![image](https://user-images.githubusercontent.com/55473846/138363184-708d291c-de7e-4135-a526-27608b8222c6.png)
This tells Nginx to use the configuration next time it is reloaded. I tested my configuration for syntax errors by typing the command below
sudo nginx -t
the following was seen 
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
this confirms that my configuration is ok and it can be seen from the screenshot below

![image](https://user-images.githubusercontent.com/55473846/138363269-7b7d2e3a-b0fc-4596-a779-19388457630a.png)
I also needed to disable default Nginx host that is currently configured to listen on port 80, for this run I ran the following command:
sudo unlink /etc/nginx/sites-enabled/default
When ready, I reloaded Nginx to apply the changes:
sudo systemctl reload nginx

![image](https://user-images.githubusercontent.com/55473846/138363417-ee9cba7f-8d30-4bed-a1e4-5f8f29a995c4.png)

My new website is now active, but the web root /var/www/projectLEMP is still empty. I created an index.html file in that location so that we can test that my new server block works as expected:
sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html

![image](https://user-images.githubusercontent.com/55473846/138363499-54b41006-7630-4dcb-a6c5-695cd2be7390.png)


Now on the browser i tried to open my website URL using IP address:
 http://ec2-18-130-125-19.eu-west-2.compute.amazonaws.com/:80
 
 ![image](https://user-images.githubusercontent.com/55473846/138363618-48c41710-c35c-4f28-90a4-0d96e22c6757.png)
 
 This above is now my temporary landing page for the application until i set up an index.php file to replace it. Once that is done I removed or rename the index.html file from my document root, as it would take precedence over an index.php file by default.
TESTING PHP WITH NGINX
My LEMP stack project is now completely set up.
Meaning that at this point my LAMP stack is completely installed and fully operational., I tested it to validate that Nginx can correctly hand .php files off to the PHP processor.
sudo nano /var/www/projectLEMP/info.php
I did this by creating a test PHP file in my document root. Open a new file called info.php within my document root in the nano text 
![image](https://user-images.githubusercontent.com/55473846/138363739-ca1d5e5e-6167-4957-8939-6db4d1ec03eb.png)

I now accessed this page in my web browser by visiting the domain name or public IP address i set up in my Nginx configuration file, followed by /info.php:
http://ec2-18-130-125-19.eu-west-2.compute.amazonaws.com/info.php

![image](https://user-images.githubusercontent.com/55473846/138363858-b2cfeb10-fa3f-47c6-ae5a-1e13a5095927.png)

As this page contains sensitive information, I ran the following command to remove it
sudo rm /var/www/projectLEMP/info.php
RETRIEVING DATA FROM MYSQL DATABASE WITH PHP 

In this step i created a test database (DB) with simple "To do list" and configure access to it, so the Nginx website would be able to query data from the DB and display it
I created a database named example_database and a user named example_user, which can be replaced with different names and different values latter if I so desire.
But first I connect to the MySQL console using the root account:
sudo mysql

![image](https://user-images.githubusercontent.com/55473846/138364026-762415bd-858f-440e-8841-0c4035d5919a.png)

This gave the example_user user full privileges over the example_database database, while preventing this user from creating or modifying other databases on the server.
Exit
I tested if the new user has the proper permissions by logging in to the MySQL console again, this time using the custom user credentials:

![image](https://user-images.githubusercontent.com/55473846/138364140-e859d10d-0cf0-40c6-94d6-8edd09d3e4bd.png)

Notice the -p flag in this command, which will prompt you for the password used when creating the example_user user. After logging in to the MySQL console, confirm that you have access to the example_database database:
SHOW DATABASES;

![image](https://user-images.githubusercontent.com/55473846/138364253-45992f7a-2290-496d-b17a-449d7764f97c.png)

Insert a few rows of content in the test table. You might want to repeat the next command a few times, using different VALUES:
mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");
![image](https://user-images.githubusercontent.com/55473846/138364352-e4796b52-a7de-49e8-8c88-8ecdaabd1a47.png)

To confirm that the data was properly entered 
SELECT * FROM example_database.todo_list;
I entered some more records into the example database.todo_list  table as show below

![image](https://user-images.githubusercontent.com/55473846/138364518-f8ca539d-b54a-449c-bcfb-1eee1436a913.png)

To confirm that the data was successfully saved to the table, run:
mysql>  SELECT * FROM example_database.todo_list;

![image](https://user-images.githubusercontent.com/55473846/138364596-307c9d9f-3d6d-40f9-b1ad-3fe0f330d311.png)
I now created a PHP script that will connect to MySQL and query for my content. Create a new PHP file in the custom web root directory using my preferred editor.:
nano /var/www/projectLEMP/todo_list.php
The following PHP script connects to the MySQL database and queries for the content of the todo_list table, displays the results in a list. If there is a problem with the database connection, it will throw an exception.
I copied this content into the todo_list.php script:
<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}
Save and close 

![image](https://user-images.githubusercontent.com/55473846/138364682-5ad7d7b9-3ee2-4b3f-863e-87968bbcb747.png)

I can now access this page in my web browser by visiting the domain name or public IP address configured for my website, followed by /todo_list.php:
http://ec2-18-130-125-19.eu-west-2.compute.amazonaws.com/todo_list.php
I saw a page like this, showing the content i have inserted in the test table

![image](https://user-images.githubusercontent.com/55473846/138364760-21189a0a-4e45-4f28-8408-53f91a5bb1e1.png)

In this Lemp-Stack implementation project I built a web-based flexible foundation for serving PHP websites and applications to visitors, using Nginx as web server and MySQL as database management system.


