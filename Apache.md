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
>>> drwxrwxrwx 1 user123 group123
( USER read|write|execute | GROUP read|write|execute | OTHER read|write|execute )
```

### Changing file/directory permissions
```
chmod permissions filename // Change Mode, change permission rwx
chmod 764 filename (absolute numberic) 
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/linux_persmission1.png)
```
chmod o=rwx test (symbolic mode)
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/linux_permission2.png)

### Changing Ownership and Group 
```
chown user123 filename          //change user
chown user123:group123 filename //change user and group
chgrp group123 filename         //change group

groups                          //show all the groups you are in
```

# Migrations Schedule 
## Workflow
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/migration_workflow.png)  
## Migration Schedule Plan 
1. Submit all fixes/changes, [QA] to verify fixes individually on QA env.
2. Define the release version number. [Product Manager]
3. Once all changes are verified, code freeze. [QA] to do full test on QA. If issues found, return to step 1.
4. If there are any data migration, the scenario should be replicated on QA env (by engineer doing the data migration script) and tested. if issues found, return to step 1.
5. Compile all changes to release note [QA] [Product Manager]
6. Submit App update to app store for approval.
7. Schedule maintenance window on Prod, all customers must be notified (Could be a system notification email).  ===> 4pm - 7pm
8. Sure Inform the CST team members [Support Team] for the go-live release plan. 
9. Merge QA branch change to PROD branch if needed (for code repository). Code freeze on QA lifted.
10. Got the release version number, “tag” (trigger tag function in SVN) for the latest commit in branch [all Dev Team]
11. During maintenance window, backup DB and conduct update to PROD servers and necessary data migration. [Backend/ Web Backend]  (Backup DB saved path and file name: /GTRIIP/backup/hh_mm_dd_mm_yyyy_{QA/PROD}_{whodidbackup}.sql)
12. Do full test on Prod using test workspaces. [QA]
13. Release version sign-off(one dev, one qa, one product sign), Just make sure everyone is kept informed.
14. If there are any data migration, the scenario should be replicated on Prod and tested.
15. If no issues found, declare end of maintenance.

## Backing and restoring db 
```
# Backing Up Db into Sql file
mysqldump -u root -p  -h 127.0.0.1 [database_name] > [file_name].sql

# Restoring DB from Sql File
create database [database_name];
mysql -u [new_user] -p [database_name] < [file_name].sql
```
https://support.hostway.com/hc/en-us/articles/360000220190-How-to-backup-and-restore-MySQL-databases-on-Linux. 
https://www.garron.me/en/articles/mysql-backup-restore.html. 
https://stackoverflow.com/questions/48392553/win-10-mysqldump-gives-error-mysqldump-got-error-1045-access-denied-for-use. 
```
git checkout branch_prod
git merge branch_qa

git mergetool
```
