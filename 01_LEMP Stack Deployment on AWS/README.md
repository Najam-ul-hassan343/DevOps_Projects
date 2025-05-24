# **LEMP Stack Deployment of a website on AWS**

The LEMP stack is a group of open-source software that is typically used together to serve dynamic web applications and websites. Each letter in LEMP stands for a different component:
L: Linux – the operating system.
E: Nginx – the web server.
M: MySQL – the database server.
P: PHP   – the server-side scripting language.

### **Why Use LEMP?**

🚀 High performance with Nginx
🛡️ Secure and reliable
🔄 Scalable for modern web apps
💡 Lightweight compared to Apache-based stacks

### **Key Steps in LEMP Stack Deployment on AWS**

Open Your AWS EC2 Instance and Log in to your AWS Management Console.
Navigate to the EC2 Dashboard.
Under Instances, select your running instance.
Note the Public IPv4 address (you will use this to connect).

![1](https://github.com/user-attachments/assets/3e44773b-5730-47c9-9232-ad794049d058)

When you launched the EC2 instance, you were prompted to download a key pair (e.g., my-key.pem).
Move this file to a secure location on your PC (e.g., C:\Users\YourName\Documents\AWS\).

⚠️ Keep this file secure and never share it.

Open Windows Terminal or PowerShell and use the ssh command:

ssh -i "C:\Users\YourName\Documents\AWS\my-key.pem" ubuntu@your-ec2-public-ip

YourName with your actual Windows username, 
my-key.pem with your actual key file name, 
ubuntu with your EC2 username (ec2-user for Amazon Linux), 
your-ec2-public-ip with your instance's public IP

Use SSH to log into the instance:
![2](https://github.com/user-attachments/assets/de155271-28e2-45a0-aa3a-28a77e6d8958)


### Setting up Nginx
To get package information from all configured sources, do **sudo apt update**
![3](https://github.com/user-attachments/assets/5f26ed5b-2aea-4909-9541-0489ae7aa52d)

**sudo apt install nginx -y**

![4](https://github.com/user-attachments/assets/42c774b8-e212-4c74-be6c-70a57dbe741f)

Use the following instructions to spin up the nginx server and make sure it launches automatically upon system reboot.

**sudo systemctl start nginx**

**sudo systemctl enable nginx**

To see if the installation was successful, run **sudo systemctl status nginx**.  The server is active when the text is green.
![5](https://github.com/user-attachments/assets/ff65af4d-00e1-4f49-9192-dd9912d1027d)

checking to see whether everything functions properly by gaining access to the default nginx web server block.  curl the DNS name localhost on any web browser on our local computer or the local IP address of our local system, which is often 127.0.0.1.
 Either curl http://localhost:80 or curl http://127.0.0.1:80

 ![6](https://github.com/user-attachments/assets/3131eece-61ba-4adb-b87e-727093370d38)

 ### **Setting up MySQL**
 
Our nginx webserver has been successfully configured, and its internet accessibility has been confirmed.  In order to store data and manage content on our web application, the next step is to install mySQL, a relational database management server.

To install MySQL-server, run **sudo apt install mysql-server** 

![7](https://github.com/user-attachments/assets/6737b220-5ba9-4b7b-a1de-ab7c1f6eff97)

Use **sudo mysql_secure_installation** to provide our MySQL server more security. This script will lock down access to our database system and remove several unsafe default settings.

![8](https://github.com/user-attachments/assets/5c5d4dc0-823c-4c09-b3fc-ca92b2c654c0)

Press Y at each prompt that appears, then enter a password and save.
Log on to the MySQL server when mysql_server has been successfully established.

**sudo mysql**

![9](https://github.com/user-attachments/assets/a6495247-15ba-47ea-b55a-6fdc82a3a5a2)

To exit from the web server we enter exit

![10](https://github.com/user-attachments/assets/a8d8ed4a-64eb-4bb1-b8fe-55ad2030e7b8)

### Setting up PHP and its Add-ons

When users submit queries to the web server, PHP is used to dynamically display the contents of our webpage.

Run **sudo apt install php-fpm php-mysql**

PHP-fpm is an acronym for PHP.  A web technology called FastCGI Process Manager is used to handle massive loads at once, improving a website's performance.

![11](https://github.com/user-attachments/assets/344b04d5-0d9d-4ff7-894c-0a1f8f0b9c11)

### Building Our Web Application's Web Server Block

Within the **/var/www/** directory, we build a directory for our project in order to serve our web content on our web server.

**sudo mkdir /var/www/myweb**  Next, we set the myweb directory's permissions to the current user system.

![12](https://github.com/user-attachments/assets/878be547-47c9-4d89-9aca-ee490bfbee8b)

Now we download the wordpress file in **/tmp** directory from **wget https://wordpress.org/latest.tar.gz**

![13](https://github.com/user-attachments/assets/c2ba717e-f0ca-4284-ad08-2fa7305296aa)

Unzip the file **latest.tar.gz** by using command: **tar -xvzf latest.tar.gz** and move the wordpress directory in **/var/www/myweb** by using command: **sudo mv wordpress /var/www/myweb**

![14](https://github.com/user-attachments/assets/f70acf8a-4c8f-4843-99b8-f200553c97c3)
![15](https://github.com/user-attachments/assets/5951e214-6eeb-4f99-a1ee-99ea63c63d8d)

**Set permissions:**

**sudo chown -R www-data:www-data /var/www/myweb/wordpress**

**sudo chmod -R 755 /var/www/myweb/wordpress**

![16](https://github.com/user-attachments/assets/3949bb35-72ac-44a1-8c0a-5e47862c4f56)

Putting our server block into configuration

**sudo nano /etc/nginx/sites-available/wordpress**

The setup needed for our web server block to function is shown in the following snippets.

![17](https://github.com/user-attachments/assets/c121d4c2-c000-45db-8ad7-2dd7b7d1c000)

 ### Create a MySQL Database and User for WordPress

Run **sudo mysql -u root -p**
![18](https://github.com/user-attachments/assets/bce738d1-9820-4908-a12d-41b652a8bf9b)

Inside MySQL prompt:

CREATE DATABASE wordpress;

CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'strongpassword';

GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';

FLUSH PRIVILEGES;

EXIT;

![19](https://github.com/user-attachments/assets/26d305ef-f8ec-4290-8a27-634a20ea935d)

The configuration file is subsequently linked to the sites-enabled directory.

**sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled**

To test our configuration for errors we run
**sudo nginx -t**
![20](https://github.com/user-attachments/assets/22a56db7-c4ee-412d-a293-5421965270a5)


























 









