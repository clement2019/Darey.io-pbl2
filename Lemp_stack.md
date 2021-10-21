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




