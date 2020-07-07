
## Ip restriction 

1) ip restrict for the whole django project   
https://pypi.org/project/django-ip-restriction/   
   
2) ip restrict for django admin only  
https://pypi.org/project/django-adminrestrict/  
  
3) Hacking into django middleware 
https://simpleisbetterthancomplex.com/tutorial/2016/07/18/how-to-create-a-custom-django-middleware.html

4) Iprestrict Apache2 
https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html#require. 
Location directive is for url  
```
---sites-available> 000-default.config------
 <Location /admin>
         Require all denied
         Require ip 122.1321.21321.321
 </Location>
```
## Ensuring Apache is upgraded to latest release version 

```
apt-get install apache2
```

 https://www.tecmint.com/apache-security-tips/


 ## Disabling Debug Error/access.log 
```
#CustomLog ${APACHE_LOG_DIR}/access.log combined
ErrorLog /dev/null
```

# Security 
## Applying security settings
Apply to both prod and qa 
```
SESSION_COOKIE_HTTPONLY = True
REMEMBER_COOKIE_HTTPONLY = True
SECURE_BROWSER_XSS_FILTER = True

SECURE_SSL_REDIRECT=True

SESSION_COOKIE_SECURE = True
SESSION_COOKIE_HTTPONLY = True

CSRF_COOKIE_SECURE = True
CSRF_COOKIE_HTTPONLY = True

X_FRAME_OPTIONS = 'DENY'
```
 ## Hiding Apache Version  
 ```
 ---- conf-avaliable >> security.conf ------
 ServerTokens Prod
 ServerSignature Off
 ```
 https://tecadmin.net/hide-apache-version-from-http-header/
 
 -----------------testing apache fix-----------------
 
 curl -I  https://yourwebsite.com

```

HTTP/1.1 302 Found

Date: Fri, 20 Mar 2020 07:51:55 GMT

Server: Apache

Location: /admin/login

X-Frame-Options: SAMEORIGIN

Vary: Cookie

Content-Type: text/html; charset=utf-8
```

