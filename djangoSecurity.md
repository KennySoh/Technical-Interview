
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
## 1. Git branch Master, QA, Master
https://medium.com/@sairamkrish/git-branching-strategy-for-true-continuous-delivery-eade4435b57e
```
git branch project_qa
git checkout project_qa
```
## 2. Ip restriction 
a) ip restrict for django admin only  
https://pypi.org/project/django-adminrestrict/  

b) Iprestrict Apache2 
https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html#require. 
Location directive is for url  
```
---sites-available> 000-default.config------
 <Location /admin>
         Require all denied
         Require ip 122.1321.21321.321
 </Location>
```
Other Option
1) ip restrict for the whole django project   
https://pypi.org/project/django-ip-restriction/   
   
2) Hacking into django middleware 
https://simpleisbetterthancomplex.com/tutorial/2016/07/18/how-to-create-a-custom-django-middleware.html

## 3. Keeping Apache2 to current stable release under ubuntu 18.04
```
apt-get install apache2
>>> apache2 is already the newest version (2.4.29-1ubuntu4.12).
```

 https://www.tecmint.com/apache-security-tips/
 
## 4. Disabling Django Restframework browsable api 
You just need to remove the browsable API renderer from your list of supported renderers for the view.

Generally:
```
REST_FRAMEWORK = {
    'DEFAULT_RENDERER_CLASSES': (
        'rest_framework.renderers.JSONRenderer',
    )
}
```
https://stackoverflow.com/questions/11898065/how-to-disable-admin-style-browsable-interface-of-django-rest-framework

## 5. Applying security settings
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

 ## 6. Hiding Apache Version  
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

## 7. Cross-site scripting [XSS]. Broswer Password autocomplete
XSS could garb the credentials from your browser. Broswer might be vunerable. 

Modern broswer
https://stackoverflow.com/questions/39462123/should-i-prevent-password-autocomplete

Added to prevent old broswers from xss
```
<input type="password" id="password" name="password" class="form-control return2submit" autocomplete="off">
```

