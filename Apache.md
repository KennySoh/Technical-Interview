# Web server
## Apache
## WSGI, Web Server Gateway Interface
WSGI stands for “Web Server Gateway Interface”. It is used to forward requests from a web server (such as Apache or NGINX) to a backend Python web application or framework. From there, responses are then passed back to the webserver to reply to the requestor.
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/webserver1.png)
  
## How to serve Django Applicaiton with Apache and mod_wsgi on Ubuntu 16.04
https://www.digitalocean.com/community/tutorials/how-to-serve-django-applications-with-apache-and-mod_wsgi-on-ubuntu-16-04

## Connect to Ubuntu server with terminal and SHH 
https://www.youtube.com/watch?v=z7jVOenqFYk  what is ssh?  
  
- to securly connect ur computer to another server through unsecrued internet. SSH conencts through a tunnel. 
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/webserver2.png)  
  
Commonly acessed via the client server model . 
PublicKey on public sever and PrivateKey on private server . 
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/webserver3.png)  

https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04 Loggin into your ubununtu instance server through ssh

```
// Can ssh with or without pem key
// https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html  (Accessing through ubuntu)

ssh ubuntu@13.23.43 // this logs in without pem but with password
ssh -i /path/my-key-pair.pem ubuntu@2001:db8:1234:1a00:9691:9503:25ad:1761 // ubuntu@12:213:12 ubuntu is the default username


```
## Pip install virtual environment and django, edit with Nano
https://www.digitalocean.com/community/tutorials/how-to-serve-django-applications-with-apache-and-mod_wsgi-on-ubuntu-16-04 (continue)   
https://stackoverflow.com/questions/14547631/python-locale-error-unsupported-locale-setting/36257050 (Local Errors).  
https://unix.stackexchange.com/questions/119358/create-file-in-folder-permission-denied (ubuntu default dont allow creation need to allow permission).  
https://phoenixnap.com/kb/access-denied-for-user-root-localhost (prevents user root)   
```
chmod u+w .
sudo nano office.py
```
## Instructions to redeploy
```
ssh kenny@11.23.41    # log in with pass
cd /home/okta/        # cd into your ubuntu
.bin/activate         # Activate venv
cd project/           # cd into Project
git pull              # pull the existing repo

mysql -u -d # loginto my sql
>>> Drop Database;
>>> Create Database;

rm - r migrations folder

./ manage.py collectstatic #create staticfolder that is reference in wsgi config folder
sudo /etc/init.d/apache2 restart #restarts apache

->Finally create superuser

Stable Version: Python3.5.2
```
## Logging errors in Apache
```
# print() in django to log errors in apache
sudo tail -f /var/log/apache2/error.log

sudo /etc/init.d/mysql restart - Restarting db
```
## Deployed Https
1) Try to keep a make of a copy of files before editing to prevent breaking it .  
2) Only alter sites-avaliable> then send files u want as symbolic links   
https://www.alibabacloud.com/help/doc-detail/102450.htm
```
sudo a2enmod ssl

sudo /etc/init.d/apache2 force-reload #reloads apache configuration file
sudo /etc/init.d/apache2 restart #restarts apache

sudo a2enmod rewrite
Redirect permanent /secure https://yourdomain.com/secure
```
## Deploment Guide
https://www.digitalocean.com/community/tutorials/how-to-serve-django-applications-with-apache-and-mod_wsgi-on-ubuntu-16-04
```
Installing Apache



```
# Udacity Full-stack Course
https://github.com/mikesprague/udacity-nanodegrees#full-stack-web-developer-nanodegree
  
## Authentication vs Authorization

# Linux 
## Ownership and Permission  
https://youtu.be/D-VqgvBMV7g. (Linux Ownership / permsission in Deatil
***
3 type of owner
- User  (Owner)
- Group (Contains Many User)
- Other (Everyone else) 
***

***
Permission
- Read  (authority to open file/ authority to ls its directory )
- Write (authority to modify file/ authority to add/rm/rename file in directory)
- Execute (authority to execute a .exe/ run a file) 
*** 
### Listing the current directory files user/owner/other permissions. 
```
ls - l  
>>> drwxrwxrwx 
( USER read|write|execute | GROUP read|write|execute | OTHER read|write|execute )
```

### Changing file/directory permissions
```
chmod permissions filename // Change Mode, change permission rwx
chmod 764 filename (absolute numberic) 
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/linux_permission1.png)
```

```
