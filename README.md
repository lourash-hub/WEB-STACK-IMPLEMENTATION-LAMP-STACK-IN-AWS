"# WEB-STACK-IMPLEMENTATION-LAMP-STACK-IN-AWS" 

###WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
Introduction
Welcome to your first Project-Based Learning (PBL) project in DevOps. This guide will walk you through implementing a LAMP Stack on AWS.

What is a Technology Stack?
A technology stack is a set of software tools and frameworks used in the development and deployment of software products. Common stacks include LAMP, LEMP, MERN, and MEAN.

Goals and Learning Outcomes
After completing this project, you will:

Be proficient in the Linux Terminal.
Understand different Web Technology stacks.
Have solid Linux administration skills.
Be familiar with AWS for hosting websites.
Be adept at using Google Search for troubleshooting.

Side Self-Study
Research and familiarize yourself with:

Software Development Life Cycle (SDLC).
The LAMP stack.
Linux commands 'chmod' and 'chown'.
TCP and UDP protocols.
Text editing in Vi (Vim) editor.
Instructions for Work Submission
Follow the provided instructions and videos for workspace setup.

Step 0 - Preparing Prerequisites
Setting up AWS and EC2 Instance
Create an AWS Account: Register and set up an AWS account. AWS Account Setup Link
Launch an EC2 Instance: Choose Ubuntu Server 20.04 LTS for your instance.
Image for reference:
Secure Your Private Key: Store your .pem file in a secure location.
Connecting to EC2 Instance (Windows)
Download Putty from Putty Download Link.
Use the following command to connect:

```bash
ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>

```
Step 1 - Installing Apache and Updating the Firewall
Install Apache:

```bash
sudo apt update
sudo apt install apache2

```
Verify Apache Installation:
```bash
sudo systemctl status apache2
```

![update-ubuntu](./Images/Apache_service.png)

Step 2 - Installing MySQL
Install MySQL:

```bash
sudo apt install mysql-server
```

log in to the MySQL console by typing:
```bash
sudo mysql
```
![MYSQL LOGIN](./Images/MYSQL_1.png)

It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1

```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
```

Exit the MYSQL Shell with 
```bash
mysql> exit
```
start the interactive script by running 
```bash
sudo mysql_secure_installation
```
This will ask if you want to configure the VALIDATE PASSWORD PLUGIN.
# Note: Enabling this feature is something of a judgment call. If enabled, passwords which don’t match the specified criteria will be rejected by MySQL with an error. It is safe to leave validation disabled, but you should always use strong, unique passwords for database credentials.
Answer Y for yes, or anything else to continue without enabling.


```bash
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:
```

If you answer “yes”, you’ll be asked to select a level of password validation. Keep in mind that if you enter 2 for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words e.g PassWord.1.

```bash
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary              file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
```

Regardless of whether you chose to set up the VALIDATE PASSWORD PLUGIN, your server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with the system root. The database root user is an administrative user with full privileges over the database system. Even though the default authentication method for the MySQL root user dispenses the use of a password, even when one is set, you should define a strong password here as an additional safety measure. We’ll talk about this in a moment.
If you enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to continue with that password. If you are happy with your current password, enter Y for “yes” at the prompt:

Estimated strength of the password: 100 
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y


For the rest of the questions, press Y and hit the ENTER key at each prompt. This will prompt you to change the root password, remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes you have made.
When you’re finished, test if you’re able to log in to the MySQL console by typing:

```bash
sudo mysql -p
```


Notice the -p flag in this command, which will prompt you for the password used after changing the root user password.
To exit the MySQL console, type:

```bash
mysql> exit
```