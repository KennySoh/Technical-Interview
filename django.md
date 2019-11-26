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

//Create a new virtual environment
virtualenv venv

//Activate
source venv/bin/activate

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
from . import views //1 Import view.py

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',views.yourownfunction); //2 on path'' , direct to implement a funciotn
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
