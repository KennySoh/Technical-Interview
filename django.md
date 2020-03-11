## Cheat Sheet, set up a new Project

```
// Create a new virtual env 
virtualenv project_venv --python=python3.6 

// Creating a new project -> cd into project_venv
django-admin startproject projectname

//Add an app to a project
python3 manage.py startapp appname

//Organise file 
- appname
	- custom_admin
	- api
		- views.py
		- urls.py
		- serializers.py
	- media
	- static
		- js
		- css
		- media
	- templates
	- admin.py
	- decorator.py
	- models.py
	- urls.py
	- utils.py
	- views.py
projectname
	-settings.py
	-urls.py
```
Configure the url 
```
---- projectname > urls.py-----
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('', include('appname.urls')),
    path('admin/', admin.site.urls),
]

---- appname > urls.py-----
from django.urls                import include,path
from .                          import views
from django.conf                import settings
from django.conf.urls.static    import static

urlpatterns = [
    path('', views.index, name='index'),
    path('user/', views.get_user, name='get_user'),
    
    path('api/', include('appname.api.urls')),
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

```

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

// Setting up requirements.txt for current environment
pip freeze > requirements.txt

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
### Recap 
#### end block tag . 
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
#### url tag . 
```
--- actual.html----
<a href="{% url 'app_name:home_index %}"> List Page</a>		  #Parsing the name path
```
```
--- urls.py-----
urlpatterns = patterns('',    
    url(r'^home$','get_home_index' ，name="home_index"),
)
```
#### static tag.
```
{% load static from staticfiles %}
<link rel="stylesheet" href="{% static 'css/layout.css' %}"> #Look in static folder...(could be inside app)
```
####  django filter
```
<p> I love <br>
```
## Django Form 
### Creating form
```
----forms.py-----
from django import forms

class SuggesionForm(forms.Form):
	name=forms.CharField()
	email=forms.EmailField()
	suggesion= forms.CharField(widgets=forms.Textarea)
```
### Sending forms to template through view
```
---views.py------
from .forms import SuggestionForm

def hello_word(request):
	return render(request, 'home.html');
	
def suggestion_view(request):
	form=forms.SuggestionForm()
	return render(request, 'suggestion_form.html',{'form':form})
```
```
---.html-----
<form action="" method="POST">
	{{ form.as_p }}
	{% crsf_token %}
	<input type="submit">
</form>
```
### Handling the submision of Form 
```
from django.contrib import messages
from django.core.mail import send_mail
from django.core.urlresolvers import reverse
from django.shortcuts import render

from . import forms 

def suggestion_view(request):
  form= forms
  if request.method == "POST":
    form = forms.SuggestionForm(request.POST)
    if form.is_valid():
      print("good form")
      send_mail(
        'Suggestion from {}'.format(form.cleaned_data['name']),   //form.cleaned_data["name"] return submitted value
        form.cleaned_date['suggestion'],      
        '{name} <{email}>'.format(**form.cleaned_data),           ///'{name}'.format(**form.cleaned_data) send in dict_form
        ['kenny@gmail.com']
      )
      messages.add_message(request, messages.SUCCESS, //Django flash emssages on screen
        'Thanks for your suggestion!')
      return HTTPResponseRedirect(reverse('suggestion'))
   return render(request, 'suggestion_form.html', {'form':form})
```

#### Custom field validation
***
- We can validate the form as whole. Use this if we need to validate two or more field in relaiton to each other. Like making sure somone gives us either a phone number Or Email or both
- We can validate individual fiels with custom cleaning methods.
- We can use Django's built-in validators or create our own. Validators are functions that take a value and return a specific error if the value is wrong.  
***   
  
##### Part1: Custom cleaning validator 
- Preventing spiders bots,  
Provide a hidden input , called a honey pot. If filled should be a bot?   
```
class SuggestionForm(forms.Form):
  name= forms.CharField()
  email = forms.EmailField()
  suggestion = forms.CharField(widget = forms.Textarea)
  honeypot = forms.CharField(required=False, widget = forms.HiddenInput, label="Leave empty") // This prevents bots

	def clean_honeypot(self):
				honeypot = self.cleaned_data['honeypot']
				if len(honeypot):
			raise forms.ValidationError('Error: Honeypot should be left empty.')
				else:
			return honeypot
```
##### Part2: Django built-in validator
```
from django.core import validators

class SuggestionForm(forms.Form):
  name= forms.CharField()
  email = forms.EmailField()
  suggestion = forms.CharField(widget = forms.Textarea)
  honeypot = forms.CharField(required=False, 
                    widget = forms.HiddenInput,
                    label="Leave empty",
                    validators=[validators.MaxLengthValidator(0)]
                   )
```
##### Part3: Django Custom validator
```
from django.core import validators

def must_be_empty(value):
  if value:
    raise forms.ValidationError('is not empty')

class SuggestionForm(forms.Form):
  name= forms.CharField()
  email = forms.EmailField()
  suggestion = forms.CharField(widget = forms.Textarea)
  honeypot = forms.CharField(required=False, 
                    widget = forms.HiddenInput,
                    label="Leave empty",
                    validators=[must_be_empty] .    // custom validator here
                   )
```

##### Cleaning a Whole Form
Checking 2 or more fields together to know if form is valid . 
- We can validate the form as whole. Use this if we need to validate two or more field in relaiton to each other. Like making sure somone gives us either a phone number Or Email or both . 

using the clean Method , def clean(self): ... This check the entire form 
```

class SuggestionForm(forms.Form):
  name= forms.CharField()
  email = forms.EmailField()
  verify_email = forms.EmailField(label="Please verify your email address")
  suggestion = forms.CharField(widget = forms.Textarea)
  
  def clean(self):
    cleaned_data =super().clean()
    email = cleaned_data.get('email')
    verify = cleaned_date.get('verify_email')
    
    if email != verify:
      raise forms.ValidationError(
        "You need to enter the same email in both fields")

```
### Models Abstract Inheritance
***
Django has 2 main type of inheritance 
- Abstract Model , cant be used for queries 
- Multi table Model
***

#### Step Abstract Model , Text and Quiz inheritate
```
class Step(models.Model):
	title = models.CharField(max_length=255)
	description = models.TextField()
	order = models.IntegerField(default = 0)
	course = models.ForeignKey(Course)
	
	class Meta:
		abstract=True
		ordering = ['order',]
	
	def __str__(self):
		return self.title

class Text(Step):
	content = models.TextField(blank = True, default='')

class Quiz(Step):
	total_questions = models.IntegerField(default = 4)
	
	class Meta:
		verbose_name_plural= "Quizzes" // Change pluralize name of registered model admin 
```
```
----views.py-----
from itertools import chain

def course_detail(request,pk):
	course = get_object_or_404(models.Course, pk=pk)
	steps = sorted(chain(course.text_set.all(),course.quiz_set.all()),
		key=lambda step:step.order)
	return render(request,'courses/course_detail.html',{
			'course':course,
			'steps':steps
		})
```
### Model Forms
Forms made from our models 
```
---forms.py----
from django import forms
from . import models

class QuizForm(forms.ModelForm):
	class Meta:
		model = models.Quiz
		fields=[
			'title',
			'description',
			'order',
			'total_questions',
		]
		exclude = [
			'course',
		]

class TrueFalseQuestionForm(forms.ModelForm):
	class Meta:
		model = models.TrueFalseQuestion
		fields = ['order', 'prompt']

class MultipleChoiceQuestionForm(forms.ModelForm):
	class Meta:
		model = models.MultipleChoiceQuestion
		fields = [
			'order',
			'prompt',
			'shuffle_answers'
		]
```
#### Using a Model Form 
```
from . import forms 

@login_required
def quiz_create(request, course_pk):
	course = get_object_or_404(models.Course, pk=course_pk)
	quizForm = forms.QuizForm()
	
	if request.method == 'POST':
		quizForm = forms.QuizForm(request.POST)
		if form.is_valid():
			quiz = quizForm.save(commit=False) //Dont put in database just make the model instance 
			quiz.course = course
			quiz.save()
			messages.add_message(request,messages.SUCCESS,"Quiz added!")
			return HttpResponseRedirect(quiz.get_absolute_url())
		return render(request , 'courses/quiz_form.html', {'form':form})
		
@login_required
def quiz_edit(request,course_pk,quiz_pk):
	quiz=get_object_or_404(modes.Quiz, pk=quiz_pk, course_id=course_pk)
	quizForm = forms.QuizForm(instance=quiz)
	
	if request.method == 'POST':
		quizForm = forms.QuizForm(instace = quiz, data=requiest.POST)
		if form.is_valid():
			form.save()
			message.success(request,"Updated {}".format(form.cleaned_data['title']))
			return HttpResponseReditect(quiz.get_absolute_url())
		return render(request,'courses/quiz_form.html', {'form':form, 'course':quiz.course}
```
### Formsets
Creating a form set
***
1. Create formset factory
```
DigitalFormset = forms.modelformset_factory( 
    models.Digital, 
    fields = ['name', 'description', 'url'],
    extra=5,       // Make five (5) products at a time , set extra and max_num to be 5
    max_num=5	
```
2. Set up the view
```
def bulk_create_products(request):
    formset = forms.DigitalFormset()
    if request.method == 'POST':
        formset = forms.DigitalFormset(request.POST)
        if formset.is_valid():
            formset.save()
            return HttpResponseRedirect(reverse('products:bulk_create'))
    return render(request, 'products/bulk_create.html', {'formset': formset})
```

***


```
-----views.py-----
def answer_form(request, question_pk, answer_pk=None):
	question = get_object_or_404(models.Question, pk=question_pk)
	formset = forms.AnswerFormSet(queryset=question.answer_set.all())
	
	if request.method == 'POST':
		formset= forms.ANswerFormSet(request.POST, queryset=question.answer_set.all())
		
		if formset.is_valid():
			answers = formset.save(commit=False)
			
			for answer in answers:
				answer.question = question
				answer.save()
			messages.success(request, "Added answers")
			return HttpResponseRedirect(question.quiz.get_absolute_url())
	return render(request, 'courses/answer_form.html', {
		'formset' : formset,
		'question':question
	})

AnswerFormSet = forms.modelformset_factory(
	models.Answer,
	form=AnswerForm,
)
```
#### Inline Model Formset
```
---.html----
{{ form.as_p }}
{{ formset.management_form }}
<table role="grid" class="stack hover" style="width: 100%">
	<thead>
		<tr>
			<th scope="col" class="text-center" style="width 10%">Order</th>
			<th scope="col" class="text-center">Text</th>
			<th scope="col" class="text-center" style="width: 10%">Correct</th>
			<th scope="col" class="text-center" style="width: 10%">Delete?</th>
		</tr>
	</thead>
	<tbody class="order">
		{% for form in formset %}
			<tr class="answer-form {% if form.instance.pk %} item {% else %} new {% endif %}">
				<td>{{ form.id }} {{ form.order }}</td>
				<td>{{ form.text }}</td>
				<td class="text-center">{{ form.correct }}</td>
				{% if form.instance.pk %}
					<td class="text-center">{{ form.DELETE }}</td>
				{% else %}
					<td class="text-center"></td>
				{% endif %}
			</tr>
		{% endfor %}
	</tbody>
</table>
			
--------views.py---------
AnswerInlineFormSet = forms.inlineformset_factory(
	models.Question,
	models.Answer,
	extra=2,
	fields=('order','text','correct'),
	formset=AnswerFormSet,
	min_num=1,
)
```

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
### Read from database and display in current html via (View.py-> Quries from db -> passed to Django Template)
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
### Create a Todo row to DB , Add a row on db from html on form submit
#### 1st Part: Create a django form and make it appear on django template
```
------1. add django form, create a forms.py------
from django import forms

class TodoForm(forms.Form):
  text = forms.CharField(max_length=40)
```

```
----2. send into template through views.py-----
from django.shortcuts import render

from .models import Todo
from .forms import TodoForm // Import created form

def index(request):
  todo_list = Todo.objects.order_by('id')
  form = TodoForm() // create an instance
  context={'todo_list' : todo_list, 'form': form}
  return render(request, 'todo/index.html', context)
```

```
-----3. Add django form into django template-----
<form action="#" method="POST" role="form">
  {% csrf_token %} // Add CRSF for safety
  <div class="form-group">
    <div class="input-group">

    <input type="text" class="form-control" placeholder="Enter todo eg. Delete junk files" aria-label = "Todo" area-describeby="add-btn"> // <--- put all this attributes into django form widget to replicate

      {{ form.text}} // Add self made form attribute
      <span class = "input-group-btn">
        <button type="submit" class="btn btn-default" id="add-btn">ADD</button>
      </span>
    </div>
  <div>
</form>
```

```
-----4. Add widget to make django form equally pretty-----
---------Form.py---------

class TodoForm(forms.Form):
  text = forms.CharField(max_length=40,
    widget=forms.TextInput(
      attrs={'class':'form-control','placeholder':'Enter todo eg. Delete junk files'}))
```
#### 2nd Part: Add the view to handle form submit, Link form submit url to view
```
-----5. Adding the view that handles Formpost data -----
---------views.py---------
from django.shortcuts import redirect // add redirect
from django.views.decorators.http import require_POST // Only accept post request

@require_POST // Only accept HTTP POST request
def addTodo(request):
  form = TodoForm(request.POST)
  print(request.POST['text']) //text is your created form field name
  
  if form.is_valid(): // LASTLY, Add to newTodo to database
    new_todo= Todo(text=request.POST['text'])
    new_todo.save()

  return redirect('index') //redirect back to index 
```

```
-----6. Add URL -----
---------urls.py---------
urlpatterns = [
  path('add', views.addTodo, name="add")
]
--------- index.html --------
<form action="{% url 'add' %}" method="POST" role="form">
```
### Update which todo is completed on mouse click
```
-----Index.html-----
{% for todo in todo_list %}
  {% if todo.complete %}
  <li class="list-group-item todo-completed">{{ todo.text }}</li>
  {% else %}
  <a href="{% url 'complete' todo.id %}"><li class="list-group-item">{{ todo.text }}</li></a>
  // Will Send to url complete/todo_id on click
  {% endif %}
{% endfor %}
```
```
----views.html----
def completeTodo(request, todo_id):
  todo = Todo.objects.get(pk=todo_id)
  todo.complete= True
  todo.save()
  
  return redirect('index')

-----urls.py------
urlpatterns=[
  path('complete/<todo_id>',views.completeTodo, name='complete')
]
```
### Delete all completed Todos
```
-----html------
<a href="{% url 'deletecomplete' %}"><buttton .....> </a>
-----urls.py------
path('deletecomplete',views.deleteCompleted, name='deletecomplete')
-----view.py-------
def deleteCompleted(request):
  Todo.objects.filter(complete__exact=True).delete()
  return redirect('index')
```
# Bootstrap Table onClick Modals appears and handle Crud 
1. Parse information using data- in Django Templates
```
------- Workign with bootstrap4 tables-----------------
<table id="dtExampleUser" class="table table-striped table-bordered table-sm" cellspacing="0" width="100%">
  <thead>
    <tr>
      <th class="th-sm" scope="col">Name</th>
      <th class="th-sm" scope="col">Usere</th>
    </tr>
  </thead>
  <tbody>
    {% for user in user_list %}                       // Django Template to parse information
    <tr data-user-id="{{ user.id }}">                 // data- html attribute to allow jquery to handle        
      <th scope="row">{{ user.name }}</th>
    </tr>
    {% endfor %}
</tbody>
```
2. Jquery to handle table tr onclick
```
$(document).ready( function () {
  $("#dtExampleUser tr").click(function(){ 
    var userId = $(this).data('user-id');   //parse user-id
  	$.ajax({  //use ajax to query entire user data with id 
  		type: "GET",
  		dataType: 'json',
  		data: {'user_id': userId , 'csrfmiddlewaretoken': $('[name="csrfmiddlewaretoken"]').val()},
  		url: "/user/get",
  		success: function (data) {
        openEditUserModal(data.personnel); //Opens Bootstrap4 Modal
      }
    });
  });
});
```
3. Handle Ajax Get user based on user.id
```
------view.py----------
from django.views.decorators.http import require_http_methods
from django.http import JsonResponse
from django.forms.models import model_to_dict
...

#Get user with id parameters
@require_http_methods(["GET"])
def get_user(request):
	user_id = request.GET.get('user_id')
	user = User.objects.get(pk=user_id)
	return JsonResponse({'user': model_to_dict(user)})
```
```
---url.py---
path('personnel/get', views.get_personnel, name='get_personnel'),
```
4. Change into Form.py 
```
-------forms.py-------
class EditUserForm(forms.Form):
    name = forms.CharField(max_length=100, widget=forms.TextInput(
      attrs={'id':'id-name','name':'name','placeholder':'Alex Lim'}))
    company_name = forms.CharField(max_length=100, widget=forms.TextInput(
      attrs={'id':'id-company-name','name':'company-name','placeholder':'Ebay-Pte-Ltd'}))

// HTTML 
<label for="name">Name</label>
{{ addUserForm.name}}


```

5. jQuery open Form on successful ajax. And pre populate
```
function openEditUserModal(user) {
  var $modal = $('.modal#editUserModal');
	$modal.find('#name').val(user.name);
  $modal.find('.edit_User_Btn').click(function() {
    $modal.find('form').attr('action','editUser/'+user.id);
  });
  $modal.find('.delete_User_Btn').click(function() {
    $modal.find('form').attr('action','deleteUser/'+user.id);

  });
	$modal.modal('show');
}
```
6.views.py handle crud functions
```
@require_POST
def editUser(request, user_id):
    # Form Validation
    form = EditUserForm(request.POST)
    if form.is_valid():
        print("Form is Valid!!!")
    # Get Form Instance and Value with cleaned data
    user = User.objects.get(pk=user_id)
    user.name=form.cleaned_data['name']
    user.company_name=form.cleaned_data['company_name']
    user.save()
    return redirect('user')
```
# Ajax and django 
```
    data = {
        'id':1,
	'name': "test",
    }
    $.ajax({
      type: "POST",
      dataType: 'json',
      data : JSON.stringify(data),
      url: "/user/update",
      success: function (result, status, xhr) {
        if (result['status'] != 'success') {
          console.log(result['message']);
          console.log(result);
          console.log(status);
          console.log(xhr);
        }
      },
      error : function(xhr, status, error){
        console.log(xhr["responseJSON"]["message"]);
        console.log(status);
        console.log(error);
  	}
    });
```

```
@require_http_methods(["POST"])
def update_user(request):
    if (True): #success
        response = JsonResponse({"message": "success"})
        return response
    else : #failuer
        response = JsonResponse({"message": "Error Message stuff not found"})
        response.status_code = 404
    return response
```

```
#Update access_group
@require_http_methods(["POST"])
def update_access_group(request):
    if (True): #success
        data = json.loads(request.body.decode())
        user_group = UserGroup.objects.get(pk=data["id"])
        user_group.name=data["name"]
        user_group.save()
        response = JsonResponse({})
        return response
    else : #failure
        response = JsonResponse({"message": "Error Message stuff not found"})
        response.status_code = 404
        return response

```

# CRSF and ajax request
https://docs.djangoproject.com/en/3.0/ref/csrf/#acquiring-csrf-token-from-html . 
```
----base.html-----
{% csrf_token %}
<script type="text/javascript">
// using jQuery
var csrftoken = jQuery("[name=csrfmiddlewaretoken]").val();
</script>
```
```
-----base.js-------
function csrfSafeMethod(method) {
    // these HTTP methods do not require CSRF protection
    return (/^(GET|HEAD|OPTIONS|TRACE)$/.test(method));
}
$.ajaxSetup({
    beforeSend: function(xhr, settings) {
        if (!csrfSafeMethod(settings.type) && !this.crossDomain) {
            xhr.setRequestHeader("X-CSRFToken", csrftoken);
        }
    }
});
```
# Django REST Framework Pretty Printed
https://www.youtube.com/watch?v=263xt_4mBNc . 
```
pip install djangorestframework
python manage.py migrate 
python manage.py createsuperuser
python manage.py startapp languages 

INSTALLED_APPS= {
	...
	'rest_framework',
	'languages'
}
```
1. Route lanaguages url 
2. Create Models 
```
class Language(models.Model):
	name= models.CharField(max_length=50)
	paradigm = models.CharField(max_length=50)
```
3. Register Language in admin.py
4. Create serializers.py 
```
----serializers.py-------
from rest_framework import serializers
from .models import Language

class LanguageSerializer(serializers.ModelSerializer):
	class Meta:
		model = Language		//link up the existing model u want to serialise 
		fields = ('id','name','paradigm')//fields u want to display
```
5. ViewSets from DRF, allow faster CRUD system 
```
----views.py----
from .models import Language
from .serializers import LanguageSerializer

class LanguageView(viewsets.ModelViewSet):
	queryset =  Language.objects.all() //get all, can changed to get filtered amount , ModelView set will take over
	serializer_class = LanguageSerializer 
```
5a. Routers, handles the url routing for DRF Viewsets
```
from . import views
from rest_framework import routers 

router = routers.DefaultRouter()
router.register('languages', views.LanguageView)

urlpatterns =[
	path('',include(router.urls))
]
```
Additional. HyperlinkedModelSerializer shows url field 
```
----serializer.py-----
class LanguageSerializer(serializers.HyperLinkedModelSerializer): //shows the url 
 class Meta:
 	model = Language
	fields = ('id','url','name','paradigm')

```
# Django REST Framework, Team treehouse
***
- Model Serializer, Makes turning queryset to json a breeze (Foreign key or file fields are a headache)
- Token based authetication, Out of the box ...
- DRF 201, 401 proper status message
***
## Installation and Setup
```
// 1. CLI installation 
pip install djangorestframework

// 2. Adding ur own app 
INSTALLED_APPS=[
	....
	'rest_framework',
	'courses',
]

//REST_FRAMEWORK = {
	'DEFAULT_AUTHETICATION_CLASSES': (
		'rest_framework.authetication.SessionAuthentication',
	),
	'DEFAULT_PERMISSION_CLASSES':(
		'rest_framework.permissions.IsAutheticatedOrReadOnly',
	)
}

// 3. add urls 
from django.conf.urls import url, include
from django.contrib import admin

urlpatterns=[
 url(r'^admin/', admin.site.urls),
 url(r'^api-auth/', include('rest_framework.urls', 
	namespace='rest_framework'))
]
```
## Model Serializers
1. add a new serializers.py 

```
from rest_framework import serializers 
from . import models 

class ReviewSerializer(serializers.ModelSerializer):
	class Meta:
		model = models.Review
```

# A Quick Intro to Model Form 
# A Quick Intro to Modal Formsets
```
---models.py-----
from django.db import models

class Example(models.Model):
	name = models.CharField(max_length=20)
	location = models.CharField(max_length=20)
```
```
---views.py----
from django.forms import modelformset_factory
from .models import Example

def index(request):
	ExampleFormSet = modelformset_factory(Example, fields=('name','location'),extra=4)
	form = ExampleFormSet(queryset=Example.objects.none())
	return render(request,'index.html',{'form':form})
```
```
----.html----
{{ form }}
```
# Admin.py registering custom admin display and editforms 
https://stackoverflow.com/questions/5947843/django-how-does-manytomanyfield-with-through-appear-in-admin

```
class TeachSubjectInline(admin.TabularInline):
    model = TeachSubject
    extra = 2 # how many rows to show

class SchoolClassAdmin(admin.ModelAdmin):
    inlines = (TeachSubjectInline,)

admin.site.register(SchoolClass, SchoolClassAdmin)
```

# Django Handling User-upload File/Image files
https://www.youtube.com/watch?v=Zx09vcYq1oc
https://gist.github.com/vitorfs/0a889e491085f6044bc328ae300b3d19
## Part 1 
***
Django File Upload
- Basic Concepts
	- Send file using POST request 
	- Set proper form encode type (enctype="multipart/form-data")
	- Files are uploaded to request.FILES
		- Dictionary-like object (eg name_of_file_object "document_name":)
		- Each file is an UploadedFile instance( Django object)
		https://docs.djangoproject.com/en/3.0/ref/files/uploads/#uploaded-files
- Configuration 
	- MEDIA_ROOT 
	- MEDIA_URL
	- Serving media files on local machines (In production suppose to be from Apache/nginx in production)
- Handling Uploaded Files 
	- File storage API - FileSystemStorage
	- Model forms fields FileField and ImageField 
	https://docs.djangoproject.com/en/3.0/ref/files/storage/#the-filesystemstorage-class ( also how to Handle File Permission)
- 
***

```
Configuration
---- settings.py ----
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'amp/media')

---- urls.py ----
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```
```
{% block content %}
	<h2> Upload </h2>
	<form method="post" enctype="multipart/form-data">
		{% csrf_token %}
		<input type="file" name="document">
		<button type="submit"> Upload file </button>
	</form>
	{% if url %}
		<p> Uploaded file: <a href="{{ url }}">{{ url }}</a></p>
	{% endif %}
{% endblock %}
```
```
Handling uploaded Files
- File storage API - FileSystemStorage
- Model form fields FileField and ImageField

-----views.py------
from django.core.files.storage import FileSystemStorage

def upload(request):
	if request.method== 'POST':
		uploaded_file = request.FILES['document']
		fs=FileSystemStorage()
		name=fs.save(uploaded_file.name, uploaded_file)
		context['url'] = fs.url(name)
	return render(request, 'upload.html',context)
```
## Part 2: Model Forms - Django File Upload
***
- Handling Uploaded Files 
	- File storage API - FileSystemStorage
	- Model forms fields FileField and ImageField 
		- FileField 
			- File saved in the file syste,
			- Saved url reference as text in the database 
			- File is not deleted if object is deleted 
		- ImageField 
			- same as file field 
***
```
----models.py----
class Books(models.Model):
	title = models.CharField(max_length = 100)
	author = models.CharField(max_length = 100)
	pdf = models.FileField(upload_to='books/pfds/')
	
	def__str__(self):
		return self.title
```
```
---views.py---
def upload_book(request):
	if request.method == 'POST':
		form =BookForm(request.POST, request.FILES)
		if form.is_valid():
			form.save()
			return redirect('book_list')
	else:
		form = BookForm()
	return render(request,'uplaod_book.html',{
		'form':form
	})

def book_list(request):
	books= Book.objects.all()
	return render(request,'book_list.html',{'books':books})
```
```
---Templates -- book_list.html---
{{ books.pdf.url }}
```

Uploading Image field 
- Similar to File Field  (pip install pillow) 

## Part 3: Class-Based Views - Django File Upload
```
----- Normal CBV ------
class BookList(View):
	def get(self, request):
	def post(self, request):
	
---- Generics------
class BookListView(ListView):
	model = Book
	template_name= "book_list.html"
	context_object_name = 'books'
```
## Deleting Uploaded Files- Django File Upload
```
def delete_book(request,pk):
	if request.method =='POST':
		book = Book.objects.get(pk=pk)
		book.delete()
	return redirect('book_list')
```
Overwriting model save/ delete
https://docs.djangoproject.com/en/3.0/topics/db/models/#overriding-predefined-model-methods
```
from django.db import models

class Blog(models.Model):
    name = models.CharField(max_length=100)
    tagline = models.TextField()

    def delete(self, *args, **kwargs):
        self.pdf.delete()
	self.cover.delete()
        super().delete(*args, **kwargs)  # Call the "real" delete() method. 
	
----- Take Note: -----
Book.objects.filter().delete() - will not trigger 

for book in Book.objects.all(): - have to delete() one by one
	book.delete() 
```
## DRF upload Files 
https://chrisbartos.com/articles/uploading-images-drf/
```
-----settings.py-------
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, "media")

------models.py--------
from django.db import models

class MyFile(models.Model):
    file = models.FileField(blank=False, null=False)
    description = models.CharField(max_lenth=255)
    uploaded_at = models.DateTimeField(auto_now_add=True)
    
------serializers.py-----
from rest_framework import serializers
from .models import MyFile

class MyFileSerializer(serializers.ModelSerializer):
	class Meta():
		model = MyFile
		fields = ('file', 'description', 'uploaded_at')
```

A view that can parse a multipart and a form so we can fully support any kind of HTML form data   
```
------views.py------
from rest_framework.views import APIView
from rest_framework.parsers import MultiPartParser, FormParser
from rest_framework.response import Response
from rest_framework import status
from .serializers import MyFileSerializer

class MyFileView(APIView):
		# MultiPartParser AND FormParser
		# https://www.django-rest-framework.org/api-guide/parsers/#multipartparser
		# "You will typically want to use both FormParser and MultiPartParser
		# together in order to fully support HTML form data."
		parser_classes = (MultiPartParser, FormParser)
		def post(self, request, *args, **kwargs):
				file_serializer = MyFileSerializer(data=request.data)
				if file_serializer.is_valid():
						file_serializer.save()
						return Response(file_serializer.data, status=status.HTTP_201_CREATED)
				else:
						return Response(file_serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

Postman Data  
```
POST : http://localhost:8000/file/upload/
{
	"file": "/media/dude_I2FPPum.jpg", (select File in the KEY-> Text, File dropdown)
	"description": "Big Lebowski",
	"uploaded_at": "2019-04-26T12:30:09.4633345Z"
}
```
## Alternative creating a seperate endpoint just for DRF file uplaod 
https://goodcode.io/articles/django-rest-framework-file-upload/
One of the things many developers do with DRF is handle file uploads the same way they handled file uploads in the old days: via as multi-part form data.   
  
Although this approach works, I would argue that sending such a request with encoded file in the body is not very RESTful. Instead, in this case I prefer my API to accept a POST or PUT request with a file being directly uploaded, with the request body being thefile content.  
  
### FileUploadParser, 
A parser in DRF is a component that takes a raw request from the client and parses it into parts. Examples of parsers include JSON parser and form parser. 
  
FileUploadParser assumes the entire request body is a single file.   
```
from rest_framework.exceptions import ParseError
from rest_framework.parsers import FileUploadParser
from rest_framework.response import Response
from rest_framework.views import APIView

class MyUploadView(APIView):
	parser_class = (FileUploadParser,)

	def put(self, request, format=None):
		if 'file' not in request.data:
		    raise ParseError("Empty content")

		f = request.data['file']

		mymodel.my_file_field.save(f.name, f, save=True)
		return Response(status=status.HTTP_201_CREATED)

	def delete(self, request, format=None):
		mymodel.my_file_field.delete(save=True)
		return Response(status=status.HTTP_204_NO_CONTENT)
```
# Working with legacy databases
https://docs.djangoproject.com/en/3.0/howto/legacy-databases/
```
python manage.py inspectdb > models_inspect.py
python manage.py inspectdb > models_inspect.py --database blah #Generate inspectdb for another database

# Copy deployed server db into local db
Using MYSQLWORKBENCH gui, Copy to clipboard> Create statement to recreate table locally. 
mysql> SHOW DATABASES;
mysql> USE webdb;
mysql> "Create statement paste "
```
# Creating an audit trail 
https://spapas.github.io/2015/01/21/django-model-auditing/

# Customizing the Django Admin
## Basic Customization
### Registering Admin 
```
class GroupAdmin(admin.ModelAdmin):
    fields = ['id', 'group','keystring']
    
admin.site.register(Group,GroupAdmin)
```
### Customizing Django Admin 
Django Source code: https://github.com/django/django/blob/master/django/contrib/admin/templates/admin/base_site.html  
  
Overwrite Django base_site.html> Save in folder similar to sourcecode to overwrite admin>base_site.html
```
{% extends "admin/base.html" %}

{% block title %}{{ title }} | {{ site_title|default:_('Django site admin') }}{% endblock %}

{% block branding %}
<h1 id="site-name"><a href="{% url 'admin:index' %}">Learning Site Administration</a></h1>  //This change django admin title 
{% endblock %}

{% block nav-global %}{% endblock %}
```
### Changing Field Order
```
class GroupAdmin(admin.ModelAdmin):
    fields = ['id', 'group','keystring']  << This changed the order
    
admin.site.register(Group,GroupAdmin)
```
## Listview, There is the List view and Detailed View
### Adding Search and Filters
```
class CourseAdmin(admin.ModelAdmin):
	inlines=[ TextInline, QuizInline]
	search_fields=['title', 'description']
	
	list_filter=['created_at','is_live']
```
### Building custom filters
```
----- admin.py------
class YearListFilter(admin.SimpleListFilter):
	title='year created'
	
	parameter_name = 'year'//link?'year'=2016
	
	def lookups(self,request, model_admin):
		return(
			('2015','2015'),
			('2016','2016'),
		)
	def queryset(self, request,queryset):
		if self.value()=='2015':
			return queryset.filter(created_at__gte=date(2015,1,1), 
						created_at__lte=date(2015,12,31))
		if self.value()=='2016':
			return queryset.filter(created_at__gte=date(2016,1,1), 
						created_at__lte=date(2016,12,31))
```
### List Display View
```
class CourseAdmin(admin.ModelAdmin):
	inlines=[ TextInline, QuizInline]
	search_fields=['title', 'description']
	
	list_filter=['created_at','is_live']
	list_display=['title','created_at','is_live'] <<< This controls the columns on list views
```

### editing the list view directly, list_editable
```
class CourseAdmin(admin.ModelAdmin):
	inlines=[ TextInline, QuizInline]
	search_fields=['title', 'description']
	
	list_filter=['created_at','is_live']
	list_display=['title','created_at','is_live'] 
	list_editable=['title','workspace']<<< This controls the columns on list views

```
## Detail view
### Customize the look and feel of view
```
class CourseAdmin(admin.ModelAdmin):
	#fields=['course','title'] have to comment out to prevent conflict with fieldset
	fieldsets=(
		(None,{
			'fields':('course','title','order','description')
			}),
		('Add content'),{
			'fields':('content',),
			'classes':('collapse',)
			}),
	)
```
### Horizontal Select and TabularInlinebuttons
```
// Changed to radio 
class CourseAdmin(admin.ModelAdmin):
	#fields=['course','title'] have to comment out to prevent conflict with fieldset
	fieldsets=(
		(None,{
			'fields':('course','title','order','description')
			}),
		('Add content'),{
			'fields':('content',),
			'classes':('collapse',)
			}),
	)

	radio_fields={'quiz':admin.HORIZONTAL}
	
// Changed from stackedinline to tablularinline
class CourseInLine(admin.StackedInline): // TablularInline
	model=models.Course
```
### Making a Text Preview
Overwrite ChangeFormField:
https://github.com/django/django/blob/master/django/contrib/admin/templates/admin/change_form.html  
Overwrite Include>Fieldset: https://github.com/django/django/blob/master/django/contrib/admin/templates/admin/includes/fieldset.html  

```Change Form Field
-----App_name>Model_name>change_form.html
-----Courses>course>change_form.html

search for fieldset.html
->{% include "admin/includes/fieldset.html" %} 
Changed to 
->{% include "admin/courses/course/includes/fieldset.html" %}
```
```Change fieldset.html
-----App_name>Model_name>includes>fieldset.html
-----Courses>course>includes>fieldset.html
{% if field.is_readonly %}
    <div class="readonly">{{ field.contents }}</div>
{% else %}
    {{ field.field }}
{% endif %}
>> Line 20: 
{% if field.field.name == 'description' %}
	<div id = "preview"></div>
{% endif %}
```

### Finishing a markdown preview
Installing external markdown previwer library

### Adding Custom Admin Actions
```
-----models.py------
STATUS_CHOICES=(
	('i','In Progress'),
	('r','In Review'),
	('p','Published'),
)

class Course(models.model):
	status=models.CharField(max_length=1,choices=STATUS_CHOICES,default='i')
```
```
-----admin.py------
class CourseAdmin(admin.ModelAdmin):
	inlines=[ TextInline, QuizInline]
	search_fields=['title', 'description']
	
	list_filter=['created_at','is_live']
	list_display=['title','created_at','is_live','status']<<< Add status into list_display
	list_editable=['title','workspace']
```
  
- Adding Admin Actions for chekcbox and Bulk Actions  
```
def make_published(modeladmin,request,queryset):
	queryset.update(status='p',is_live=True)
	
make_published.short_description= "Mark selected courses as Published" // Adding the message for the drop down 

class CourseAdmin(admin.ModelAdmin):
	inlines=[ TextInline, QuizInline]
	search_fields=['title', 'description']
	
	list_filter=['created_at','is_live']
	list_display=['title','created_at','is_live','status']
	list_editable=['title','workspace']
	actions=[make_published]<<< Add funciton into respective admin

```
