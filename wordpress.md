# Wordpress

## MAMP Overview

My Apache , My SQL, PHP  
  
wordpres/wp-admin  
phpMyAdmin -> Database  

Themes + Plugin +  

## Wordpress.org (Self-hosted wordpress) vs Wordpress.com(Hosted solution)
Install Classic Editor.  
   
Appearance-> Customize   
Pages-> All Pages  
  
Classic editor vs Block Editor

BlockEditor-> Convert to block
Classic editor is only for older themes 

## Tools and domains, FTP

SiteGround-> 
wpdevcourse.com student sandbox
ks.kennysoh@gmail.com
  
FTP- fie transfer protocol (Local to online)  
FileZilla  
sftp - chrome extension  
   
Pdf Excel  
Image optimiation  
Payment (Stripe , Paypal)  

## Using Local now...
While I originally used MAMP, as I teach in the current course videos, I now use Local by Flywheel instead, and I recommend that you do the same. Like MAMP, Local is also free to use, and you don't need a Flywheel hosting account to use it. There are some fundamental differences, and advantages to using Local by Flywheel instead of MAMP. The most obvious is that Local is designed for use with WordPress, and has an auto-installer so you can get new websites up and running very quickly. My websites in Local also seem to work and load faster than sites on MAMP. Another advantage of Local is the included email server, so you can test email sent from your websites.  

## Hosting
- Shared Hosting - share with resources, site monitoring to prevent , sitegorund shared hosting program
- Dedicated Servers or private servers. 
- Virtual private server,VPS- Partition into seperate disk space
- Cloud Hosting, Allow a group of hosting as web designer
- Managed wordpress hosting (Flywheel, normamlly faster expensive , includes their own cache)

## Local by flywheel , Local Mamp 
***
- posts (blog, has categories and tags)
- pages (designed to be static pages, Setting-> reading -> set Homepage)
- appearance -> Customizer
***

File structure  
***
 - Local Sites-> practice0site01 -> app -> public
    - wp-config-sample (Normally have to change to wp-config if installing manually)
 - Database -> Local by fly wheel adminer  
    - wp users, wp options  
 ![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/wp1.png) 
 - wp-content
    - themes, plugins , uploads ( Only this change nothing else in the file structure change)
***
## Siteground , Managed hosting by flywheel
***
- My Account
    - Primary Domain, Go to C panel
    - Auto installer wordpress, 
    - Setting , Timezone, lanaguage
    - Media setting, uncheck organise my media by date
    - Permalink Settings -> Postname
***

