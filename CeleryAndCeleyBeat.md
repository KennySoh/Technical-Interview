# Installing celery is a task-queue in python. (Can be used with Django)
```
Install redis in docker. 
Install celery in an existing django/ python project


pip install celery

CELERY_BROKER_UR= 'redis://127.0.0.1:6379'
CELERY_ACCEPT_CONTENT = ['application/json']
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TASK_SERIALIZER = 'json'
CELERY_TIMEZONE = 'Asia/Singapore' 
```

# Create a new celer.py file
```
-- create a celery.py---
from celery import Celery
from django.conf import settings

os.environ.setdefauly('DJANGO_SETTINGS_
```
