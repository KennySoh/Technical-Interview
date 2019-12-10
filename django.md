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
  
After creating project, python dependecy so other people can run the git clone software on their environment . 
https://medium.com/python-pandemonium/better-python-dependency-and-package-management-b5d8ea29dff1  
  
  
## Setting up Django Project With MySQL
https://www.digitalocean.com/community/tutorials/how-to-create-a-django-app-and-connect-it-to-a-database
1. Creating the django skeleton refer above

2. Settings.py
```
TIME_ZONE = 'America/New_York'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
ALLOWED_HOSTS = ['your server IP address']
```

3. Install MySQL Database Connector . 
In order to use MySQL with our project, we will need a Python 3 database connector library compatible with Django. So, we will install the database connector, mysqlclient, which is a forked version of MySQLdb.  
```
sudo apt-get install python3-dev
sudo apt-get install python3-dev libmysqlclient-dev
pip install mysqlclient
sudo apt-get install mysql-server
```

4. Create the Database . 
```
systemctl status mysql.service //Verify that MySQL service is running
mysql -u db_user -p //my sql login 

mysql> SHOW DATABASES;

mysql> CREATE DATABASE blog_data;
- Query OK, 1 row affected (0.00 sec)


```
5. Add the MySQL Database Connection yo your Application . 
```
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '',
        'USER': '',
        'PASSWORD': '',
        'HOST': 'localhost',
        'PORT': '3306',
```
6. Test MySQL Connection to Application
```
python manage.py runserver your-server-ip:8000
```

## MYSQL
```
//Logging in to mysql db
mysql -u root -p //Key in password
> SHOW DATABASES;
> CREATE DATABASE nus_amp;
```
This is are django default database tables on intial setup.  using MySQLWorkbench to see.   
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django10.png) 
## Django MVT isntead of MVC
Normal Model View Controller .  
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django8.png)    
Model View Template, Django is different in that it controls the own View themselves.    
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django9.png)    

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
## URL Patterns
## Views 
## Multiple Apps
```
----setting.py----
INSTALLED_APPS= (
  'django.contrib.admin',
  'courses',
)

....
TIME_ZONE="",

```
# Django Models
Django ORM, Object relational mapper.
Each model is a table, each attribute is a column in a table. When u add new instances the orm creates a new row in a table. 

***
-firstproject
  - newapp
    - models.py (here)
  - firstproject
***

```
class Course(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    title = models.CharField(max_length=255)
    description = models.TextField()
```
- Make migration and migrate whenever u change models . 

## Adding instances from the manage.py shell
```
-----terminal----
python manage.py shell
>>> from courses.models import Course
>>> Course.objects.all()
[]
>>> type(Course.objects.all())
<class 'django.db.models.query.QuerySet>
>>> c = Course()
>>> c.title = "Python Basics"
>>> c.description = "Learn the basics of Python"
>>> c.save()
>>> Course.objects.all()
[<Course: Course object>]
>>> exit()

python manage.py shell
>>>
>>> Course.objects.create(title="Object-Oriented Python", description="Learn about Python's classes")
<Course: Course object>
```

```
// Adding __str__ returns the specified string on django query. 

---models.py---
class Course(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    title = models.CharField(max_length=255)
    description = models.TextField()
    
    def __str__(self):
      return self.title
      
 ---terminal---
python manage.py shell
>>> from courses.models import Course
>>> Course.objects.all()
[<Course: Python Basics>, <Course: Python Collections>, <Course: Object-Oriented Python>
```
## First App View
1. add view.py
```
---app> view.py---
from django.shortcuts import render

from .models import Course

def course_list(request):
  courses = Course.objects.all()
  output=','.join([str(course) for course in courses])
  return HtttpResponse(output)
```
2. add app> urls.py
```
from django.cong.urls import url
from . import views

urlpatterns=[
  url(r'^courses/',include('courses.urls')),
  url(r'^$', views.course_list),
]
```
## Adding instance on Django Admin
***
- go to admin page , www.localhost/admin
- create superuser
- register model on admin
***
```
---terminal---
python manage.py createsuperuser
- username:
- pass:
```
```
--- register new model on newapp>admin.py---
from django.contrib import admin
from .models import Course

admin.site.register(Course)
```

## Templates
***
-firstproject
  -firstproject
  - newapp 
    - templates
      - courses
        - course_list.html
***

```
--- course_list.html ---
{% for course in courses %}
<h2>{{ course.title }}</h2>
{{ course.description }}
{% endfor %}
```
```
---app>views.py---
from django.http import HttpResponse
from django.shortcuts import render
from .models import Course
 
def course_list(request):
  courses = Course.objects.all()
  return render(request, 'courses/course_list.html', {'courses': courses})
```
```

// Add outer template folder
***
- firstproject
  - template
    -home.html
  - firstproject
  - newapp
      - templates
        - courses
          - course_list.html
***
//Change settings to tell django to look for templates in specificapp folder
--settings.py---
TEMPLATES = [
  {
    'BACKEND': 'django.template.backends.django/DjangoTemplates',
    'DIRS':['templates'],
    'APP_DIRS':True,
    'OPTIONS': {
        'context_processors':[
          'django.template.context_processprs.debug',
          ...
        ],
    },
  },
]
```
## Template inheritance
```
---layout.html---
{% extends "layout.html" %}
{% block urowntitle%} Well hello there!{% endblock urowntitle %}

{% block urowncontent %}
<h1> Welcome</h1>
{% endblock urowncontent%}
```

Example:
We want to use our base.html template. Please add an {% extends %} tag to the article_list.html template.
```
---articles/templates/articles/article_list.html---
{% extends "base.html" %}
{% for article in articles %}
{{ article.headline }}
{% endfor %}
```
https://docs.djangoproject.com/en/1.7/topics/templates/#template-inheritance
```
---base.html---
<!DOCTYPE html>
<html lang="en">
<head>
    <link rel="stylesheet" href="style.css" />
    <title>{% block title %}My amazing site{% endblock %}</title>
</head>

<body>
    <div id="sidebar">
        {% block sidebar %}
        <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/blog/">Blog</a></li>
        </ul>
        {% endblock %}
    </div>

    <div id="content">
        {% block content %}{% endblock %}
    </div>
</body>
</html>
```
This template, which we’ll call base.html, defines a simple HTML skeleton document that you might use for a simple two-column page. It’s the job of “child” templates to fill the empty blocks with content.
```
---child template----
{% extends "base.html" %}

{% block title %}My amazing blog{% endblock %}

{% block content %}
{% for entry in blog_entries %}
    <h2>{{ entry.title }}</h2>
    <p>{{ entry.body }}</p>
{% endfor %}
{% endblock %}
```
## Static Assets
```
---settings.py---
STATIC_URL = '/static/'
STATICFILES_DIRS = (                //add new static file dirs
  os.path.join(BASE_DIR,'assets'),  
)
```
```
---urls.py---
from django.contrib.staticfiles.urls import staticfiles_urlpatterns

...
urlpatterns=[
  url(r'^courses/', include('courses.urls')),
]

urlpatterns += staticfiles_urlpatterns() //check if we are in DEBUG mode in setting.py ? yes, they add a static path.
```
```
{% load static from staticfiles %}
<!doctype html>
<html> 
  <head>
    <title>{% block title %}{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'css/layout.css' %}">
  </head>
  <body>
    {% block content %}{% endblock %}
   </body>
</html>
```
## Django let us create smaller forms inside the admin form for model with InLine
``` 
---admin.py---
from django.contrib import admin
from .models import Course, Step

class StepInline(admin.StackedInline): // there stacked and tabular add this 
  model = Step

class CourseAdmin(admin.ModelAdmin):
  inlines = [StepInline,]
  
admin.site.register(Course, CourseAdmin)
admin.site.register(Step)
```

## Add a Detail View
click a course name and see all the steps
```
--- from django.shortcuts import render ---

def course_detail(request, pk): //pk=primary key, django know its the primarykey
    course = Course.objects.get(pk=pk)
    return render(request, 'courses/course_detail.html', {'course':course})
```

```
---url.py---
from . import views

urlpatterns = [
  url(r'(?P<pk>\d+)/$',views.course_detail);
]
```

Now we need to create the view. I've already made the URL and template for you.  
  
Create a view named writer_detail that takes a pk argument. It should .get() the Writer with the requested pk and render() the "articles/writer_detail.html" template. Provide the Writer in the context as "writer".

```
from django.shortcuts import render

from .models import Article, Writer


def article_list(request):
    articles = Article.objects.all()
    return render(request, 'articles/article_list.html', {'articles': articles})

def writer_detail(request, pk):
    writer = Writer.objects.get(pk=pk)
    return render(request, "articles/writer_detail.html", {'writer': writer})
```
## Ordering and 404s
what if we get our steps out of order? what if someone puts in a bad URL?
```
--models.py---
class Step(models.Model):
  class Meta: //adding Meta , to set default ordering ...normally set by id
    ordering =['order',]
  def __str__(self):
    return self.title
```
django 500 - python500 when theres an exception. need to throw a 404 when a bad url, such as non-existing pk is entered. 

## Step Detail View
```
---view.py---
from .models import Course, Step

def step_detail(request, course_pk, step_pk):
  step = get_object_or_404(Step, course_id=course_pk, pk=step_pk)
  return render(request, 'courses/step_detail.html', {'step':step})
```
```
---url.py---

urlpatterns = [
  url(r'(?P<course_pk>\d+)/$', views.course_detail),
]
```

Finally, we want to make sure we handle bad pks when looking up our Articles. Use get_object_or_404 to look up the Article. You'll need to import it from django.shortcuts.
```
---urls.py---
from django.conf.urls import url
from django.shortcuts import get_object_or_404

from . import views

urlpatterns = [
    url(r'writer/(?P<pk>\d+)/$', views.writer_detail),
    url(r'article/(?P<pk>\d+)/$',views.article_detail),
    url(r'', views.article_list),
]
```

```
---views.py---
from django.shortcuts import render,import get_object_or_404

from .models import Article, Writer


def article_list(request):
    articles = Article.objects.all()
    return render(request, 'articles/article_list.html', {'articles': articles})


def writer_detail(request, pk):
    writer = Writer.objects.get(pk=pk)
    return render(request, 'articles/writer_detail.html', {'writer': writer})

def article_detail(request, pk):
    article= get_object_or_404(Article, pk=pk)
    return render(request, 'articles/article_detail.html', {'article':article})
```

## Template Inheritance
Template tags . 
- end block tag . 
```
---base.html-----
<h1>{% block title %} {% endblock %}</h1>

<main>
{% block content %}{% endblock %}
</main>
```
```
---actual.html-----
{% extends "base.html" %}
{% block title %} Well hello there!{% endblock title %}
{% block content %} <h1> Welcome ! </h1> {% endblock content %}
```
- url tag . 
```
--- actual.html----
<a href="{% url 'views.hello_world' %}"> Hello World Page </a>
<a href="{% url 'app_name:home_index %}"> List Page</a>
```
```
--- urls.py-----
urlpatterns = patterns('',    
    url(r'^home$','get_home_index' ，name="home_index"),
)
```
- static tag.
- django filter

# Meet Peewee, Our ORM( python databases topic
```
pip install peewee

peewee is a python tool for orms
```
### Modeling
```
from peewee import *

db = SqliteDatabase('students.db')

class Student(Model):
  username = CharField (max_length =255, unique =True)
  points =IntegerField(default =0)
  
  class Meta: //tell them what database they belong too, what field should be index, what order
    database = db
if __name__ == '__main__':
  db.connect()
  db.create_tables([Student], safe=True)
  
sqlite3 students.db
> .tables
> select * from student
> .exit
```
### Queries are your friend
***
- .create()
- .select()
- .save()
- .get()
- .delete_instance()
***
```
from peewee import *

db = SqliteDatabase('students.db')

class Student(Model):
  username = CharField (max_length =255, unique =True)
  points =IntegerField(default =0)
  
  class Meta: //tell them what database they belong too, what field should be index, what order
    database = db
    
students=[
  {'username' : 'kenny',
   'points':100},
  {'username' : 'kenny',
   'points':100},
  {'username' : 'kenny',
   'points':100},
  {'username' : 'kenny',
   'points':100},
]

def add_students():
  for student in students:
      try:
        Students.create(username= student['username'],
                        points = student['points'])
      except IntegrityError:
        student_record = Student.get(username=student['username'])
        student_record.points =student['points']
        student_record.save()

def top_student():
   student = Student.select().order_by(Student.points.desc()).get()
   return student

if __name__ == '__main__':
   db.connect()
   db.create_tables([Student], safe=True)
   add_students()
   print("Our top student right now is :{0.username}.".format(top_students())) //0 is what is return by format

if __name__ == '__main__':
  db.connect()
  db.create_tables([Student], safe=True)
```

# Pretty printed Tutorials
https://www.youtube.com/watch?v=r9kT-jm136Q
## Django Models 
```
------------ Models------------
from django.db import models

class GithubAccount(models.Model):
  name =CharField(max_length=20)

class Company(models.Model):
  name =CharField(max_length=20)
  
  def __str__(self):               //(Take not 2 underscores __)
    return self.name


class Language(models.Model):
    name= models.CharField(max_length=20)
    
    def __str__(self):
      return self.name
      

class Programmer(models.Model):
   name = models.CharField(max_Length = 20 )
   githubaccount= models.OneToOneField(GithubAccount, on_delete = models.CASCADE, primary_key=True,) // One to One
   company= models.ForeignKey(Company, on_delete = models.CASADE) //( Many to one relationship, Many Programmer to One Com)
   languages = models.ManyToManyField(Language) //( Many to many relationship put on object that makes more sense)
   
   def __str__(self):
      return self.name


```

```
------------ Creating, Updating , Deleting, Reading from Database ------------
Python shell 
>>> from yourapp.models import Company

// Creating
>>> google = Company(name="Google")
>>> google.save()

// Update
>>> google.name="Alphabet"
>>> google.save()

// Delete
>>> google.delete()
(1, {'yourapp.Company':1}) // Tells u what got delted

// Read
>>> apple= Company.objects.get(pk=2)
>>> apple
<Company: Company object (2)>

------------ Creating objects with foreign key ------------
>>> anthony = Programer (name= 'Anthony', company=apple)
>>> anthony.save()

// Getting its foreign key 
>>> anthony.company   // (from object with foreign key in attribute) 
<Company: APPLE>
>>> apple.programmer_set.all()  // (from object without foreign key attribute)
<QuerySet [<Programmer :Stacy>, <Programmer : Kelly>]>

------------ Many to many relationship, Django automatically creates adjoining table ------------
>>> anthony = Programmer.objects.get(pk=1)
>>> stacy = Programmer.objects.get(pk=2) // Create 2 Programmer
>>> python = Language(name='Python')
>>> java = Language(name='Java') // Create 2 Language

>>> anthony.languages.add(python) // Adding Langauges <-> Programmer . this adds to the adjoining table
>>> anthony.languages.add(ruby)
>>> stacy.languages.add(python)
>>> stacy.languages.add(ruby)

>>> anthony.save() //Possibly have to save
>>> stacy.save()

// Reading 
>>> anthony.languages.all() //Programmer has ManytoMany Attribute
<QuerySet [<Language: Java>, <Language :Haskell>]>
>>>python.programmer_set.all() //Language does not have the ManyotMany Attribute
<QuerySet [<Programmer: Anthony>, <Programmer :Stacy>]>
```
## Django Models, A better Many to Many relationship 
https://docs.djangoproject.com/en/3.0/topics/db/models/#extra-fields-on-many-to-many-relationships  
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/django_model1.png) .  
```
---Membership becomes the ajoining table instead and store person and group related data)
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=128)

    def __str__(self):
        return self.name

class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(Person, through='Membership')

    def __str__(self):
        return self.name

class Membership(models.Model):
    person = models.ForeignKey(Person, on_delete=models.CASCADE)
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    date_joined = models.DateField()
    invite_reason = models.CharField(max_length=64)
```
## Django Queries. 
https://www.youtube.com/watch?v=WimXjp0ryOo . 
```
python shell
>>> Company.objects 
<django.db.models.manager.Manager object at 0x7fc38259sd> // This parse the manager object that we use to query

>>> Languages.objects.all()
<QuerySet [<Language : Python>, <Language : Java>]>

>>> languages=Languages.objects.all()
>>> languages[0]
<Language: Python>

>>> languages[0].name
'Python'
>>> languages[0].date_created
datetime.date(1999, 2, 20)

-------- Usign Filter or Exclude---------
>>> Language.objects.filter(name_exact="Python") //<QuerySet [<Language:Python>]>
>>> Language.objects.filter(name_iexact="Python") // Not case sensitive
>>> Language.objects.exclude(name_exact="Pyhton") // Return all Queryset except for name="Python"
>>> Language.objects.filter(age_gt=25) //returns greater than 25 , (gt,lt,gte,lte)
>>> Programmer.objects.filter(name__contains="nt")
>>> Programmer.objects.filter(name__icontains="nt") // Not case sensitive, depends on Db, Sqlite doesnt have case sensitive
>>> Programmer.objects.filter(name__startswith="Jan")
>>> Programmer.objects.filter(name__istartswith="jan")
>>> Programmer.objects.filter(name__endswith="Jan")
>>> Programmer.objects.filter(name__iendswith="jan")
>>> Programmer.objects.filter(age__isnull=True)
>>> Programmer.objects.filter(name__isnull=False)
>>> Programmer.objects.count() // return 26
>>> Programmer.objects.filter(name_isnull=False).count() // return 6

//.get() returns Query, But only can have one item. >more than 1 or 0 will return error
>>> Language.objects.filter(name_exact="Python").get() // <Language:Python>
>>> Programmer.objects.all()[:5] // O-index to 5-1 Index
>>> Programmer.objects.all() [5:5] // returns none, 5-index to 5-1index 
>>> Programmer.objects.all() [5:10] // returns none, 5-index to 10-1index 

>>> Company.objects.filter(date_created__gt='1990-01-01') //returns company created greater than '1990-01-01'
>>> Company.objects.order_by('age')
>>> Company.objects.order_by('-age')
```
## Django To Do App, 
### Registering Models on Admin
```
----admin.py-----
from django.contrib import admin

from .models import Todo

admin.site.register(Todo)
```
### read from database and display in current html via (View.py-> Quries from db -> on Django Template)
```
------view.py-----
from .models import Todo

def index(request):
    todo_list = Todo.objects.order_by('id')
    form = TodoForm()
    context = {'todo_list' : todo_list, 'form' : form}
    return render(request, 'todo/index.html', context)
```
```
----todo/index.html--------
<ul class="list-group t20">
  {% for todo in todo_list %}
    {% if todo.complete %}
    <li class="list-group-item todo-completed">{{ todo.text }}</li>
    {% else %}
    <a href="{% url 'complete' todo.id %}"><li class="list-group-item">{{ todo.text }}</li></a>
    {% endif %}
  {% endfor %}
</ul>
```
