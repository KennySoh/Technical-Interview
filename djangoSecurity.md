
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
Broswers version might be vunerable. When they use password managers to store password on the broswer local cache.
Bad Hates , XSS could grabb the credentials from your browser with a js script. 

Modern broswer
https://stackoverflow.com/questions/39462123/should-i-prevent-password-autocomplete

Added to prevent old broswers from xss
```
<input type="password" id="password" name="password" class="form-control return2submit" autocomplete="off">
```
## 8. Password Strength 
Using Django Build in Password Validator ensure
```
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
        'OPTIONS': {
            'min_length': 9,
        }
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]
```
Making sure its included in API serializers , if you are using apis to create/reset password 
```
class UserPasswordResetSerializer(serializers.ModelSerializer):
	class Meta:
		model = User
		fields = ['id', 'password']

	def update(self, instance, validated_data):
		user = super().update(instance, validated_data)
		try:
			user.set_password(validated_data['password'])
			user.save()
		except KeyError:
			pass
		return user
		
	def validate_password(self,value):
		validate_password(value)
		return value
```

## 9. Session Security
 Django Security for session timeout  
https://django-session-security.readthedocs.io/en/latest/quick.html 
  
```
SESSION_SECURITY_EXPIRE_AFTER = 3600 #seconds
SESSION_EXPIRE_AT_BROWSER_CLOSE = True
```
## 10. Prevent Concurrent Logins
https://pypi.org/project/django-preventconcurrentlogins/

## 11. Configuring Different Django Environment
https://thinkster.io/tutorials/configuring-django-settings-for-production

Settings File Structure.  
```
|-yourapp/
|_|-settings/
|__|-base.py
|__|-dev.py
|__|-prod.py
|__|-qa.py
|-manage.py
|-requirements.txt
|-.gitignore
```
  
For qa.py and prod.py. 
```
from yourapp.settings.base *

DEBUG = False

SECRET_KEY = os.environ['SECRET_KEY']

# SECURITY WARNING: update this when you have the production host
ALLOWED_HOSTS = ['0.0.0.0', 'localhost']
```

Change manage.py and wsgi.py 
```
os.environ.setdefault("DJANGO_SETTINGS_MODULE", "yourapp.settings.dev")
```

Set the local environment variables for your respective servers on CLI
```
export DJANGO_SETTINGS_MODULE=yourapp.settings.dev		#Set Environment Variables
export SECRET_KEY="32jokokgokowkoO(#@)49302jifje_=32ionjr"

printenv 			#List of Environment Variables
unset DJANGO_SETTINGS_MODULE	#Remove Environment Variables
```
Set the qa/prod environment   
https://stackoverflow.com/questions/46891408/django-setting-environment-variables-in-etc-apache2-envvar-is-not-working.  
https://stackoverflow.com/questions/51430759/how-to-specify-environment-variables-in-apache-site-config-for-django.  
```
-----------apache2.conf------------
SetEnv DJANGO_SETTINGS_MODULE 'yourapp.settings.qa'
SetEnv SECRET_KEY '123456778877'

-----------Django> wsgi.py---------
import os

from django.core.wsgi import get_wsgi_application

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "yourapp.settings.base")

_application = get_wsgi_application(). <---- Modified

def application(environ, start_response): <----- Added
    # pass the WSGI environment variables on through to os.environ
    os.environ['DJANGO_SETTINGS_MODULE'] = environ['DJANGO_SETTINGS_MODULE']
    os.environ['SECRET_KEY'] = environ['SECRET_KEY']
    return _application(environ, start_response)
    
-----------settings > qa.py-----------
SECRET_KEY = os.environ['SECRET_KEY']

```
