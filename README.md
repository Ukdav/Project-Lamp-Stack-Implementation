## PROJECT-LAMP-STACK-IMPLEMENTATION

**Introduction to Web Stack Implementation (LAMP Stack) on AWS**

Building and deploying web applications in the cloud has become increasingly essential in today's digital landscape. Amazon Web Services (AWS) offers a robust and flexible platform for hosting web applications, and one of the most popular web stack configurations on AWS is the LAMP stack.

The LAMP stack, which stands for Linux, Apache, MySQL (or MariaDB), and PHP, is a tried-and-true combination of software components that provides a powerful foundation for developing and hosting web applications. AWS, as a leading cloud service provider, offers a comprehensive set of tools and services that make it easy to set up, scale, and manage LAMP stack environments.

In this context, Linux serves as the operating system, Apache act as the web server, MySQL (or MariaDB) handles the database management, and PHP is the scripting language that facilitates dynamic web content generation. This stack is known for its stability, versatility, and open-source nature, making it an ideal choice for a wide range of web applications.

In this guide, we'll explore the key steps involved in implementing a LAMP stack on AWS, from launching a Linux-based EC2 instance to configuring Apache, setting up the database, and deploying PHP-based web applications. We'll also discuss best practices for security, scalability, and performance optimization to ensure a reliable and efficient web hosting environment in the AWS cloud.

Whether you're a developer looking to host your web application, a system administrator tasked with managing web infrastructure, or a business owner seeking to leverage AWS for your online presence, understanding how to implement a LAMP stack on AWS is a valuable skill that can help you harness the full potential of cloud computing for web development.

**A LAMP Stack is a solution stack that is being used in deploying web applications. It stands for Linux, Apache, MySql, PHP, Perl or Python.**

1. Linux: This is an operating system that serves as the backbone of the LAMP Stack, and it is actively used in deploying other components.

2. Apache: is a web server software which via HTTP requests processes requests and transmits information via the internet.

3. MySQL: used for creating and maintaining dynamic databases. It supports SQL and relational tables and provides a DBMS(Database Management System).

4. PHP, PERL, or PYTHON: This represents programming languages that effectively combine all the elements of the LAMP stack and are used to make web applications execute.

## CREATION OF EC2 INSTANCE IN AWS

First, we log on to AWS Cloud Services and create an EC2 Ubuntu VM instance. When creating an instance, choose keypair authentication and download the private key(*.pem) on your local computer.

![ec2 instance n](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/f570ef6f-f528-49ec-8089-61e3a78f5d90)

On the Git bash terminal, cd into the directory containing the downloaded private key, you can rename the file if you choose. Run the below command to log into the instance via ssh:

_cd Downloads_

_SSh -i projectpem.pem ubuntu@16.170.148.177_

![cd download and ssh -i command](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/19e0f21f-e8f3-4315-9f9e-88d8184ebe05)

successfully logged into the ec2 instance via SSH using git bash.

## SETTING UP THE APACHE2 WEB SERVER VIA UBUNTU PACKAGE MANAGER

Setting up an Apache2 Server via the Ubuntu Package Manager is a fundamental process for web server administration on Ubuntu-based systems. This concise summary provides an overview of the key steps involved:

**Summary:**

Setting up an Apache2 Server on Ubuntu using the package manager is a straightforward process. First, ensure you have the necessary prerequisites, including a Ubuntu server with sudo privileges. Then, follow these essential steps:

1. **Installation:** Use the package manager (typically apt) to install Apache2, ensuring you have the latest version.

2. **Basic Configuration:** Customize your server by setting up virtual hosts, modifying the default web page, and managing server files.

3. **Security:** Prioritize server security by implementing best practices, such as firewall rules and SSL/TLS encryption.

4. **Performance Optimization:** Optimize Apache2's performance using configuration tweaks and caching mechanisms.

5. **Troubleshooting:** Be prepared to troubleshoot common issues using the available resources and expertise.

By following these steps, you'll have a secure and efficient Apache2 web server ready to host your websites or web applications on your Ubuntu system.

To deploy the web application, we need to install Apache via Ubuntu package manager apt:

# Updating the packages

*$ sudo apt update*

*$ sudo apt install apache2*

![sudo apt update](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/95dcf48b-4116-48b6-8f0b-422cfefde1da)

![sudo apt install apache2](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/faa5ae88-3a35-422b-909d-2d85f978aa23)

To verify that Apache2 is running as a service on our OS, you will use the following command:

# Starting apache2 Server

*$ systemctl start apache2*

# Ensuring Apache2 starts automatically on the system boot

*$ systemctl enable apache2*

*$ sudo systemctl status apache2*

![sudo apache2 status check](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/07790850-2d4f-4536-bb18-1f6e09120a8c)

If it shows a green text, it means the web server has been successfully spunned and is live.

## CONFIGURING SECURITY GROUP INBOUND RULES ON EC2 INSTANCE  

Configuring Security Group Inbound Rules is a critical aspect of securing Amazon Elastic Compute Cloud (EC2) instances. Security Groups act as virtual firewalls that control inbound and outbound traffic to your EC2 instances.

When the instance is created, we have a default TCP rule on port 22 opened which is useful for SSH connection to a terminal. In order to ensure that our webpage are being accessed on the internet, we need to open a TCP port 80 inbound rule.

![inbound rules](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/e13cae9b-84fd-48cf-8870-5b1230bb9df9)

To check the accessibility of our web server on the internet, we curl the IP address/DNS name of our localhost.

curl http://127.0.0.1:80  or curl http://localhost:80

![curl on localhost](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/b42bfbe5-f187-4a23-9a2b-16c296e9657b)

To see if our web application server can respond to requests, use the public IP address of our instance on a web browser. 

*http://16.170.148.177/:80*

![apache2 server webpage](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/0711ebdf-dae7-419e-941f-992393e8e13e)

## INSTALLING MYSQL

MySQL on an Ubuntu Server is a popular relational database management system used for storing, managing, and retrieving structured data. Ubuntu provides a straightforward and well-supported environment for MySQL, making it a reliable choice for web applications, data-driven projects, and various software solutions. Administrators can easily install, configure, and maintain MySQL on Ubuntu Server using the package manager, and developers can leverage its powerful features and robust performance to build scalable and efficient database-driven applications. Additionally, the open-source nature of both Ubuntu and MySQL ensures cost-effectiveness and a vibrant community for support and updates.

Install MySQL using the *$ sudo apt install mysql* command.

![installing mysql server](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/ef6df1f9-2a27-46a6-84f5-72d876235d1b)

using the *$ sudo mysql*; This will connect to the MySql server as the administrative database user root, which is inferred by the use of sudo when running the command.

![msql console status](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/845fad2e-4a4b-4f0f-aa78-724c1b4cde44)

Use the *$ sudo mysql_secure_installation* command to remove insecure default settings and enable protection for the database.

when you are done, test if you are able to log into the **MySql** console by typing *$ sudo mysql -p*

![sudo msql -p](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/e8e5636f-7d4e-44db-8d0a-7ad4d6e3fdbc)

Note: The -p flag in this command, which will prompt you for the password used after changing the root user password.

![sudo mysql_secure_installation](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/68c4b7a0-1d52-4efc-9cc0-6ac01cc2412a)

Exit from the MySQL terminal by typing exit.

![exit](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/2ba0c3d9-9dab-4f7d-ae08-3cbfafc35a50)

## INSTALLING PHP AND ITS MODULESPHP serves as a programming language that is useful for dynamically displaying the contents of the webpage to users who make requests to the web server.

We need to install php alongside its modules, php-mysql which is a PHP module that allows PHP to communicate with the MySQL database, and libapache2-mod-php which ensures that the Apache web server handles the php contents properly.

* $ sudo apt install php php-mysql libapache2-mod-php*

![installing PHP](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/ccfd77c6-a495-4180-b1ab-3eebdcb0d633)

On successful installation of PHP and its modules, we can check the version to see if it was properly installed.

![php -v](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/c6ff9451-de5f-4d20-8ec0-3be930629f5f)

## CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

We set up a virtual host using Apache to enable us to deploy our web content on the webserver. Apache's virtual hosting ensures that one or more websites can run on a web server via different IP addresses.

![11 apache_virtualhost_architecture](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/217e8f26-3c1b-43f0-80b5-5f373e04e757)

## CREATING WEB DOMAIN FOR OUR SITE 

Apache webserver serves a website by way of server blocks inside its /var/www/ directory, and it can support multiple of these server blocks to host other websites.

Here we create a new directory called projectlamp inside the /var/www/ directory.

*$ sudo mkdir /var/www/projectlamp*

![sudo mkdir](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/5c947c9e-2bf3-43d1-aaba-fb540037abd7)

Then we change the permissions of the project lamp directory to the current user system.

*$ sudo chown -R $USER:$USER /var/www/projectlamp*

![sudo chown](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/ef80ed8e-9fab-429f-a946-044fd1b84fe1)

The projectlamp directory represents the directory that will contain files related to our website as it represents a new server block on the Apache webserver. In order to spin up this server block we need to configure it by creating a .conf file.

sudo vi /etc/apache2/sites-available/projectlampstack.conf

The following represents the configuration needed to spin up the server block. Copy and paste into the editor.

![virtual host](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/e01ca8d8-bec6-4e04-8a11-419761dee12e)

Run esc :wq  to save and terminate vi editor.

Run sudo a2ensite projectlamp to activate the server block.

Run sudo a2dissite 000-default to deactivate the default web server block that comes with Apache on default.

Reload the apache2 server sudo systemctl reload apache2

![final stage](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/416d0bb2-a1f0-4ac2-84f0-73c2e7d1386e)

Now go to your browser and open URL using the public IP address and the Public DNS IP :

*http://16.170.148.177:80* 

![php webpage](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/0bdf5649-517a-4d2b-b168-6381bc02a8d0)

*ec2-16-170-148-177.eu-north-1.compute.amazonaws.com*

![dns](https://github.com/Ukdav/Project-Lamp-Stack-Implementation/assets/139593350/24e594b2-fcd6-4288-aca3-43b85d99af2d)

In conclusion, implementing a LAMP (Linux, Apache, MySQL, PHP/Perl/Python) stack is a powerful and widely adopted solution for building robust web applications and hosting dynamic websites. The combination of Linux as the operating system, Apache as the web server, MySQL as the relational database, and a choice of scripting languages like PHP, Perl, or Python provides a versatile and flexible environment for developers and administrators.

With Ubuntu as the foundation, LAMP offers a secure, stable, and open-source platform that can be tailored to specific project requirements. Apache serves as a reliable web server, capable of handling high traffic loads and supporting various web technologies. MySQL provides efficient data storage and retrieval, while the scripting language enables dynamic content generation and web application development.

The LAMP stack's open-source nature encourages collaboration, ensures cost-effectiveness, and benefits from a vast community of developers and users. Implementing a LAMP stack on a server provides the tools and infrastructure needed to create, deploy, and manage modern web applications, making it a time-tested choice for many web development projects.








































































