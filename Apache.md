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
https://stackoverflow.com/questions/14547631/python-locale-error-unsupported-locale-setting/36257050 (Local Errors)
https://unix.stackexchange.com/questions/119358/create-file-in-folder-permission-denied (ubuntu default dont allow creation need to allow permission)
```
chmod u+w .
```
# Udacity Full-stack Course
https://github.com/mikesprague/udacity-nanodegrees#full-stack-web-developer-nanodegree
  
## Authentication vs Authorization
