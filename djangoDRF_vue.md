## Section 2:Build Your First Rest Api with django

- Api 
  - Rest, is the most common mechanism
- JSON
- Endpoints, urls patterns to access the api

```
/tweets/
/tweets/536727
/tweets/536727/hashtags
```
## Restful API 
- Request, Response Message
- HTTP Verbs (GET, POST, PUT DELETE)

## Request Messages and Response
- 200 OK

## Your First Django API - part one
```
models

class Manufacturer(models.Model):
  name=models.CharField(max_length=120)
  location =models.CharField(max_length=120)
  active= models.BooleanField(default=True)
  
  def __str__(self):
    return self.name

class Product(models.Model):
  manufacturer = models.ForeignKey(Manufacturer,on_delete=models.CASCADE,related_name="products")
  name=models.CharField(max_length=120)
  description= models.TextField(blank=True,null=True)
  photo = models.ImageField(blank=True,null=True)
  price=models.FloatField()
  shipping_cost=models.FloatField()
  quantity = models.PositiveSmallIntegerField()
  
  def __str___(self):
    return self.name
```

```
------------views using generic views------------------
from django.views.generic.detail import DetailView
from django.views.generic.list import ListView

from .models import Product, Manufacturer

class ProductDetailView(DetailView):
  model= Product
  template_name = "products/product_detail.html"

class ProductListView(ListView):
  model=Product
  template_name="products/product_list.html"
```

```
from django.urls import path
from .views import ProductDetailView, ProductListView

urlpatterns = [
  path("",ProductListView.as_view(), name="product-list"),
  path("products/<int:pk>/",ProductDetailView.as_view(), name="product-detail")
]
```
```
-------template---------------
<img src="{{ object.photo.url }}" alt="product photo">
```
## Your First Django api part2
***
Setup 2 endpoints for our API
1) will allow users to retrieve information about a specific product instance
2) will allow users to retrieve a list of all the avaliable products
***
```
----views.py-----
def product_list(request):
  products = Product.objects.all()
  data = {"products":list(products.values("pk","name"))}
  response = JsonResponse(data)
  return response
  
def product_detail(request,pk):
  try:
    product=Product.objects.get(pk=pk)
    data={"product:"{
    "name":product.name,
    "manufacturer":product.manufacturer.name,
    "description":product.description,
    "photo":product.photo.url,
    }}
  except Product.DoesNotExist:
    response= JsonResponse({
      "error":{
        "code":404,
        "message":"product not found!"
    }},
    status=404)
  return response
```
```
---- urls.py ----
path("api/products/",views.product_list,name="product-list"),
path("api/products/<int:pk>/",product_detail,name="product-detail")
```
--- Json Response, Not the best way ... we only get first_bike.jpg doesnt give us image.url or manufacturer name--- 

# DRF Level One 
***
- How to use DRF to create REST APIs
- Understand the concept of serialization and deserialization
- How to use the Serializer and ModelSerializer classes
- How to create Function/Class Based API Views
- WHat the Browsable API is and how to use it
- Define Validation criteria for user input
- How to properly represent nested relationships between entities with DRF
***

its a package to include in existing django
## Downloading drf
```
pip install django
pip install djangorestframework
django-admin startproject newsapi
```
```
INSTALLED_APPS =[
  ...
  'rest_framework',
]
```
## Serializers
Serializers allow complex data such as querysets and model instances to be converted to native Python data types that can be rendered into useful formats like JSON: this process is known as Serialization of Data. 

Serializer also provide deserailization. Also talk about Parsers and Renderers
```
---create a serializer.py inside api folder----
from rest_framework import serializers
from new.models import Article

class ArticleSerializer(serializers.Serializer):
  id = serializers.IntegerField(read_only = True)
  author = serializers.CharField()
  title = serializers.CharField()
  description = serializers.CharField()
  body = serializers.CharField()
  location = serializers.CharField()
  publication_data = serializers.DateField()
  active = serializers.BooleanField()
  created_at = serializers.DateTimeField(read_only=True)
  updated_at = serializers.DateTimeField(read_only=True) #read_only because django controls this
  
  def create(self,validated_data):
    print(validated_data)
    return Article.objects.create(**validated_data)
  
  def update(self,instance,validated_data):
    instance.author= validated_data.get('author', instance.author)
    instance.title= validated_data.get('title',instance.title)
    instance.description=validated_data.get('description',instance.description)
    instance.body = validated_data.get('body',instance.body)
    instance.location=validated_data.get('location',instance.location)
    instance.publication_date=validated_data.get('publication_date',instance.publication_date)
    instance.active=validated_data.get('active',instance.active)
    instance.save()
    return instance
```


```
------------Python Shell , using serializers ----------
python manage.py shell
>>> from news.models import Article
>>> from news.api.serializers import ArticleSerializer
>>> article_instance = Article.objects.first()
>>> serializer = ArticleSerializer(article_instance)
>>> serializer
ArticleSerializer(<Article: John Doe Happy Birthday ISS>):
  id= IntegerField(read_only =true)
  ....
>>> serializer.data       #This returns python native datatype.A Dictionary 
{'id':1,'author':'JohnDoe','publication_date':'2019-02-21','created_at':'2019-02-21T15:10:59.873736z','updated_at':'2019-02-21T15:10:59.874787z'...}
>>> from rest_framework.renderers import JSONRenderer
>>> json=JSONRenderer().render(serializer.data)  #Change dict into Json
>>> json
b'{"id:1,"author":"John Doe","title":"Happy Birthday ISSL200"...}

-----------deserialization------------------
>>> import io
>>> from rest_framework.parsers import JSONParser
>>> stream = io.BytesIO(json)
>>> data = JSONParser().parse(stream)
>>> data          # Python dictionary
{'id':1,'author':'John Doe' ....} 
>>> serializer = ArticleSerializer(data=data)
>>> serializer.is_valid()     #make sure it valid
>>> serializer.validated_data 
>>> serializer.save()         #Creates another query
```
## @api_view Decorator Part One
***
Django REST Framework provides two wrappers we can use to write API Views:
- The @api_view decorator, for working with Function Based API Views
- The APIView class, for working with Class Based API Views
***
These wrappers provide a few bits of functionality such as making sure you receive Request instances in your view, and adding context to Response objects so that content negotiation can be performed.  
  
The wrappers also provide behaviour such as returning 405 Method Not Allowed responses when appropriate, and handling any ParseError exception that occurs when accessing request.data with malformed input . 
  
We will also look at **Browsable API** .   
  
***
1) create-api folder 
2) Create views.py
```
from rest_framework import status
from rest_framework.decorators import api_view
from rest_framework.response import Response

from news.models import Article
from news.api.serializers import ArticleSerializer

@api_view(["GET"])
def article_list_create_api_view(request):
  if request.method == "GET":
    articles = Article.objects.filter(active=True)
    serializer = ArticleSerializer(articles, many=True) // "many=True" is when u are sending serializer a query Set
    return Response(serializer.data)
```
***
