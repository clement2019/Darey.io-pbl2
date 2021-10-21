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
