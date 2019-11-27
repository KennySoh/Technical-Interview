## Cheat Sheet

```
// Creating a new project
django-admin startproject projectname

//Add an app to a project
python3 manage.py startapp appname

//Starting the server
python3 manage.py runserver

//creating migrations 
python3 manage.py makemigrations

//migrate the database
python3 manage.py migrate

//creating a Super User for the admin panel
pyhton3 manage.py createsuperuser

//collecting static files into one folder
python3 manage.py collectstatic

//checking current version
python3
>>> import django
>>> django.VERSION
(2, 0, 0, 'final', 0)

```
## Downloading Django & Starting first project
```
pip3 install django //Newest verison
pip3 install django==2.0.2 //Specific verison

django-admin help
django-admin startproject firstProject // Create a new project

python3 manage.py runserver // Starts server 127.0.0.1:8000
```
## Python virtual environment
```
//Install pip3
sudo apt-get install -y python3-pip

//Install virtual env
sudo pip3 install virtualenv

//Put ur virtual env next to ur project
cd Desktop/urProject

//Create a new virtual environment
virtualenv venvName

//Activate
source venvName/bin/activate

//Deactivate
deactivate
```
## Setup and Existing Django Project
```
1. Grab a copy of the project
git clone new_project.git

2. Create a virtual environment and install dependencies
virtualenv venv
source venv/bin/activate
pip3 install -r requirements.txt

3. Enter your database settings in settings.py. (Enter mysql to ensure it corresponds)

5. Initialize your database.
python3 ./manage.py migrate

6. If your App has a custom user model, you'll need to create a new superuser for the admin
python3 ./manage.py createsuperuser

7. Run the development server to verify everthing is working
python3 ./manage.py runserver
```
## MYSQL
```
//Logging in to mysql db
mysql -u root -p //Key in password
> SHOW DATABASES;
> CREATE DATABASE nus_amp;
```
## Git ignore file
***
-firstProject
  -firtProject
  -.gitignore, http://gitignore.io/api/django
  ```
  # Created by https://www.gitignore.io/api/django
  # Edit at https://www.gitignore.io/?templates=django

  ### Django ###
  *.log
  *.pot
  *.pyc
  __pycache__/
  local_settings.py
  db.sqlite3
  db.sqlite3-journal
  /media  
  /static
  ```
***

## Django File Structure
***
- firstProject
  - firstProject
    - __init__.py
    - settings.py (base directory, secret_key, debug=True to allow debugging-false when production,middleware, root_url,templates,wsgi_application, databases)
    - urls.py (url patterns, routing)
    - wsgi.py (For hosting)
  - manage.py
  - db.sqlite3
***
## Url
Url Patterns let us configure the routing. 
```
--- url.py---
from django.contrib import admin
from django.urls import path, include
from django.conf.urls import url
from . import views //1 Import view.py

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',views.yourownfunction); //2 on path'' , direct to implement a funciotn
    
    url(r'^admin/', include(admin.site.urls)), //aternative way to add url.
    url(r'^$',views.index),
    
]

```
3. Create view.py in the same directory with ur specific funcitons
```
--- view.py---
from django.http import HttpResponse

def yourownfunction(request):
  return HttpResponse('<h1> Hello </h1>')
```
## Seperation of HTML code using Templates
This compartmentalise url patterns to url.py, function handling to view.html, front end to home.html.
***
- firstproject
  - templates // 1 (create new top level folder)
    - home.html // 2 (create home.html)
  - firstproject
  - manage.py
  -db.sqlite3
***

```
--- view.py--- ownCreated.py
from django.http import HttpResponse
from django.shortcuts import render //3 import render

def yourownfunction(request):
  return render(request,'home.html')
  
def your ownfunction2(request):
  return HttpResponse('<h1> Hello </h1>')
```

```
--- home.html--- ownCreated.html
<h1> Random HTML </h1>

```
## Django {{dictkey}} , render(request, 'home.html',{'dictkey','value'})
Inserting dynamic text in html.
```
--- view.py--- ownCreated.py
from django.http import HttpResponse
from django.shortcuts import render

def yourownfunction(request):
  return render(request,'home.html',{'dictkey':'value'}) // 1. place the dictionary, key value pairing
  
def your ownfunction2(request):
  return HttpResponse('<h1> Hello </h1>')
```

```
--- home.html--- ownCreated.html
<h1> Random HTML {{dictkey}}</h1> //2 Django automatically inserts value into keys.
```
## Form: Creating a Form, And handling submit. Linking everything. 
***
1. add url routing direct to function
2. add view.py function to custom.html & parse variables & get request details
3. declare custom.html
***
```
--- home.html---
<form action="{%url 'count'%}"> // 1 make it link to url name="count"
  <textarea cols="40" rows="5" name="fulltext"></textarea>
  <br/>
  <input type="submit" value="Count!" />
</form>
```
```
--- url.py---
from django.contrib import admin
from django.urls import path, include
from . import views //1 Import view.py

urlpatterns = [
    path('', views.homepage),
    path('countpath/',views.count,name="count"); //2 add routing
]
```

```
--- view.py---
from django.http import HttpResponse
from django.shortcuts import render

def homepage(request):
  return render(request,'home.html') 

def count(request):
  return render(request,'count.html') //3 render count.html
```
```
--- count.html---
<h1>Count </h1> //4 Declare count.html
```

### Form: Counting the words from Form
Counting the word from the request object

```
// After submiting form variable name="fulltext" is passed through the link. 
www.youtube.com/?fulltext=eggs&var2=something
```

```
--- view.py---
from django.http import HttpResponse
from django.shortcuts import render

def homepage(request):
  return render(request,'home.html') 

def count(request):
  fulltext = request.GET['fulltext'] //1. get the fulltext variable from the request, link ?fulltext=eggs
  print(fulltext)
  wordlist=fulltext.split()
  return render(request,'count.html',{'fulltext':fulltext,'count':len(wordlist)})  //2. parse variables
```

```
--- count.html---
<h1>There are {{ count }} words </h1>  //3. insert count of words

<h1> Your Text</h1>
{{ fulltext }}                         //4. insert original text
```

### Form: Creating a dictionary that show which word appear the most.
Topic: Django template {% for loop}, Parsing dict, list
```
--- view.py---
from django.http import HttpResponse
from django.shortcuts import render
import operator

def homepage(request):
  return render(request,'home.html') 

def count(request):
  fulltext = request.GET['fulltext'] 
  wordlist=fulltext.split()
  worddictionary={}
  
  for word in wordlist: // 1. add into dictionary
    if word in worddictionary:
      #increase
      worddictionary[word] +=1
    else: 
      #add to the dictionary
      worddictionary[word]=1
      
  sortedWords=sorted(worddictionary.items(),key=operator.itemgetter(1), reverse=True) //optional sort the list of tuple based on second tuple, countperword.. pass this if u want
      
  return render(request,'count.html', {'fulltext':fulltext,'count':len(wordlist),'worddictionary':worddictionary.items()}) //2. worddictionary.items() into list of key,value tuple
```

```
--- count.html---
<h1>There are {{ count }} words </h1>  

<h1> Your Text</h1>
{{ fulltext }}     

<h1> Word Count: </h1>
{% for word, countperword in worddictionary %}  //Django Templating for loop 

{{ word }}
<br />
{{ countperword }}
<br />

{% endfor %}
```

## Compartmentalise website to > 2 apps
```
python manage.py startapp blog
python manage.py startapp job
```
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django1.png)

## Models
***
- firstProject
  - jobs
    - models.py
  - firstProject
***

```
---models.py----
from django.db import models

class Job(models.Model):
  image = models.ImageField(upload_to='images/')
  summary = models.CharField(max_length=200)
```
Django Model field reference: https://docs.djangoproject.com/en/2.2/ref/models/fields/#imagefield . 
  
1. Once you change your Model , You need to apply migration
```
python manage.py migrate // getting databse up to speed
```
```
----setting.py----
INSTALLED_APPS = [
  'jobs.apps.JobsConfig', // add the autogenerated class from jobs>app.py, after migrate
  'django.contrib.admin,
 
]
```
```
----jobs>app.py----
from django.apps import AppConfig

class JobsConfig(AppConfig):
  name='jobs'
```
2. add media path so when us ave media it will go here
```
----settings.py----
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```
```
python manage.py makemigrations // will create model Job
pip install Pillow // if stuck

python manage.py migrate
```

## Admin
```
// www.localhost/admin enter the django admin
python manage.py createsuperuser
Username : kenny
Email address: ks.kennysoh@gmail.com
Password: something
```
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django2.png)  
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django3.png)   

```
---jobs>admin.py---
from django.contrib import admin 

from .models import Job

admin.site.register(Job) 
```
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django4.png)  
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django5.png)   

Add url to link to media 
``` 
from django.contrib import admin
from django.urls import path
from django.conf import settings
form django.conf.urls.static import static

---url.py---
urlpatterns = [
  path('admin/', admin.site.urls),
] + static(settings.MEDIA_URL, document_root = settings.MEDIA_ROOT)
```

## Posgres
postgress.app

sql  
Server:  
Database:  
Port:  
Username:   
Password:   

- One Database per project . 
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django6.png)  
- Make migration when u have a change database. Cause all the model and data lives in the old one. 

## Adding a new app
***
1. Add model
  - Title, Pub_date, Body, images
2. Add blog app to the setting
3. Create a migration
4. Migrate
5. Add to the admin
***

1. Add model 
```
----newapp>models.py----
from django.db import models

class Blog(models.Model):
    title = models.CharField(max_length=255)
    pub_date = models.DateTimeField()
    body = models.TextField()
    image = models.ImageField(upload_to= 'images/')
```

2. Add new blog app to the setting
```
---setting.py---
INSTALLED_APPS = [
    'blog.apps.BlogConfig',
    'jobs.apps.JobsConfig',
    'django.contrib.admin'.
    'django.contrib.auth',
    ....
]
```
3. Make migration
4. Migrate
```
python manage.py makemigrations
python manage.py migrate
```
5. Add to the admin
```
---new app> admin.py---
from django.contrib import admin
from .models import Blog

admin.site.register(Blog)
```
## Adding homepage 
***
1. Add url 
2. Add views
3. Directory
***

1. Add url
```
import jobs.views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',jobs.views.home,name="home"),
] + static(settings.MEDIA_URL, document_root = settings.MEDIA_ROOT)
```

2. add views
```
--jobs> views.py----
from django.shortcuts import render

def home(request):
    return render(request, 'jobs/home.html')
```
3. Directory  
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django7.png) 

# Django Team tree house
## What are URL Patterns
```
------ urls.py ------
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^admin/', include(admin.site.urls)),
    url(r'^$',views.index),
]
```
```
------ views.py ------
```

