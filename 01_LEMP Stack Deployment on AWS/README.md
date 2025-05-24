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

![2](https://github.com/user-attachments/assets/1665d816-6281-4790-86c0-f498f4406435)

### Install Nginx

![3](https://github.com/user-attachments/assets/449e24da-6c71-4cd8-b859-ed23acbadd67)
![4](https://github.com/user-attachments/assets/e3969afe-57da-44bf-8a7b-a95a04833ce3)

 Check the status mysql is running or not.

 ![5](https://github.com/user-attachments/assets/dc859656-df8f-4d65-aa46-0d33efd2c36b)

 









