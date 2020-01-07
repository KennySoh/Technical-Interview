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
---create a serializers.py inside api folder----
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
https://www.django-rest-framework.org/tutorial/2-requests-and-responses/

***
1) create-api folder 
2) Create views.py
```
from rest_framework import status
from rest_framework.decorators import api_view
from rest_framework.response import Response

from news.models import Article
from news.api.serializers import ArticleSerializer

@api_view(["GET","POST"])
def article_list_create_api_view(request):
  if request.method == "GET":
    articles = Article.objects.filter(active=True)
    serializer = ArticleSerializer(articles, many=True) // "many=True" is when u are sending serializer a query Set
    return Response(serializer.data)
  
  elif request.method == "POST":
    serializer = ArticleSerializer(data=request.data)
    if serializer.is_valid():
      serializer.save()
      return Response(serializer.data, status =status.HTTP_201_CREATED)
    return REsponse(serializer.errors, status = status.HTTP_400_BAD_REQUEST)
```
***

## @api_view Decorator Part Two
```
@api_view(["GET","PUT","DELETE"])
def article_detail_api_view(request,pk):
  try:
    article=Article.objects.get(pk=pk)
  except Article.DoesNotExist:
    return Response({"error":{
                      "code":404,
                      "message":"Article not found!"
                    }}, status =status.HTTP_404_NOT_FOUND)
                    
 if request.method == "GET":
    serializer = ArticleSerializer(article)
    return Response(serializer.data)
 elif request.method=="PUT":
    serializer = ArticleSerializer(article, data = request.data)
    if serializer.is_valid():
      serializer.save()
      return Response(serializer.data, status=status.HTTP_201_CREATED)
    return Response(serilizer.errors, status.HTTP_400_BAD_REQUEST)
 elif request.method=="DELETE":
    article.delete()
    return Response(status=status.HTTP_204_NO_CONTENT)
```
```
-----url-----
from news.api.view import (article_detail_api_view)
path("articles/<int:pk>/",article_detail_api_view, name="article-detail")

```

## APIView Class
Class Based Views . Fall in line with DRY principles
```
from rest_framework import status
from rest_framework.decorators import api_view
from rest_framework.views import APIView . // Include APIView 
from rest_framework.response import Response

from news.models import Article
from news.api.serializers import ArticleSerializer

class ArticleListCreateAPIView(APIView):
  
  def get(self, request):
    articles= Article.objects.filter(active=True)
    serializer = ArticleSerializer(articles,many=True)
    return Response(serializer.data)
  
  def post(self,request):
    serializer = ArticleSerializer(data = request.data)
    if serializer.is_valid():
      serializer.save()
      return Response(serializer.data, status=status.HTTP_201_CREATED)
    return Response(serilizer.errors, status.HTTP_400_BAD_REQUEST)
 
class ArticleDetailAPIView(APIView):
   
   def get_object(self,pk):
     article = get_object_or_404(Article, pk=pk)
     return article
   
   def get(self,request,pk):
     article = self.get_object(pk)
     serializer = ArticleSerializer(article)
     return Response(serializer.data)
   
   def put(self, request, pk):
      article =self.get_object(pk)
      serializer = ArticleSerializer(article, data = request.data)
      if serializer.is_valid():
        serializer.save()
        return Response(serializer.data, status=status.HTTP_201_CREATED)
      return Response(serilizer.errors, status.HTTP_400_BAD_REQUEST)
   def delete(self, request, pk):
      article =self.get_object(pk)
      article.delete()
      return Response(status = status.HTTP_204_NO_CONTENT)
```
```
-----url-----
from news.api.view import (ArticleDetailAPIView,ArticleListCreateAPIView)
urlpatterns=[
  path("articles/",ArticleListCreateAPIView.as_view(),name="article-list"),
  path("articles/<int:pk>/",ArticleListCreateAPIView,as_view(), name="article-detail")

```
## Serializers Validation
if any error occur the, **.error** property will contain a dictionary with the corresponding error messages:  
```
serializer = ContactSerializer(data={'body':'some text', 'email':'name#gmail.com'})
serializer.is_valid() # Returns False
serializer.errors     # Returns {'email':[u'Enter a valid e-mail address.']}
```
  
We are going to see how to specify custom validation checks for our models and serializers using both **Field-Level Validation** and **Object-Level Validation** . 
  
### Built in Validators
https://www.django-rest-framework.org/api-guide/validators/#uniquevalidator

### Object Level Validation vs Field Level Validation
- Object Level -> check on multiple fields 
- Field Level Validation-> check on single fields 

### Custom Validators- Object Level Validation
```
----serializer.py----

  def validate(self,data):
    """ Check that description and title are different """
    if data["title"] == data["description"]
       raise serializers.ValidationError("Title and Description must be different")
    return data
```

Result of error return
```
HTTP 400 Bad Request

{
 "non_field_errors":[
    "Title and Description must be different from one another!"
  ]
}
```
### Custom Validators- Field Level Validation
```
----serializer.py----

  def validate_title(self,value):
    if len(value)<60:
       raise serializers.ValidationError("The title has to be at least 60 characters long")
    return value
```
Result of error return
```
HTTP 400 Bad Request
{
 "title":[
    "The title has to be at least 60 chars long!"
  ]
}
```
# Model Serializer Class
### Basic Model Serializer . 
```
from rest_framework import serializers
from news.models import Article

class ArticleSerializer(serializers.ModelSerializer):

  class Meta:
    model = Article
    fields = ("title","description", "body")
```  
  
### Model Serializer with additional field time since publication   
```
from datetime import datetime
from django.utils.timesince import timesince
from rest_framework import serializers
from news.models import Article
 
class ArticleSerializer(serializers.ModelSerializer):

  time_since_publication = serializers.SerializerMethodField()

  class Meta:
    model = Article
    fields = ("title","description", "body")

  def get_time_since_publication(self,object):
    publication_date = object.publication_date
    now = datetime.now()
    time_delta = timesince(publication_date,now)
    return time_delta
```
```
-----Python Shell------
python manage.py shell
>>> from news.api.serializers import ArticleSerializer
>>> serializer = ArticleSerializer()
>>> print(repr(serializer))
ArticleSerializer():
  time_since_publication = SerializerMethodField() . //Includes this additional field
  author = CharField(max_length =50)
  ...
```
### Model Serializer with validation errors
Same as Custom validators. 
```
class ArticleSerializer(serializers.ModelSerializer):

  time_since_publication = serializers.SerializerMethodField()

  class Meta:
    model = Article
    fields = ("title","description", "body")

  def get_time_since_publication(self,object):
    publication_date = object.publication_date
    now = datetime.now()
    time_delta = timesince(publication_date,now)
    return time_delta
    
  def validate(self,data): #Object-Level Validators
    """ Check that description and title are different """
    if data["title"] == data["description"]
       raise serializers.ValidationError("Title and Description must be different")
    return data
    
  def validate_title(self,value):  #Field-Level Validators 
    if len(value)<60:
       raise serializers.ValidationError("The title has to be at least 60 characters long")
    return value
```
# Nested Relationships in our Serializer Classes
how to define **Nested Relationships** in our Serializer Classes!  
```
---models.py-----
class Journalist(models.Model):
  first_name=models.CharField(max_length=60)
  last_name=models.CharField(max_length=60)
  biography=models.CharField(max_length=60)

  def __str__(self):
  return f"{ self.first_name }"

class Article(models.Model):
  author = models.ForeignKey(Journalist, on_delete=models.CASCADE, related_name="articles")
  title = models.CharField(max_length=120)
  description = models.CharField
```
Json Returns
```
/api/articles/
[
  {
    ...,
    "author":1  #primary key for foreign key
  },
  {
    ...,
    "author":2 
  }
]
```
## Showing name of author(foreignkey) instead of primary key
Option1 . 
```
class ArticleSerializer(serializers.ModelSerializer):

  time_since_publication = serializers.SerializerMethodField()
  author = serializers.StringRelatedField() # Include this
  ...
```
Json Returns
```
/api/articles/
[
  {
    ...,
    "author":"John",
  },
  {
    ...,
    
    "author":"John",
   }
]
```
Option 2 . **(When creating need to include Author...not ideal)**
Requires author when creating Article....
Result in constraint error when author sets as "read_only=true"
```
Class JournalistSerializer(serializers.ModelSerializer):
  class Meta:
    model = Journalist 
    fields = "__all__"
    

class ArticleSerializer(serializers.ModelSerializer):

  time_since_publication = serializers.SerializerMethodField()
  author = JournalistSerializer()
  ...
```
Json Returns
```
/api/articles/
[
  {
    ...,
    "author":{
        "id":1,
        "first_name":"John",
        "last_name":"Titor",
     }
  },
  {
    ...,
    
    "author":{
        "id":1,
        "first_name":"John",
        "last_name":"Titor",
     }
   }
]
```  
Option 3- Most ideal
```
---serializer.py nested serializers---
Class JournalistSerializer(serializers.ModelSerializer):
  articles = ArticleSerailizer(many=True, read_only=True)
  
  class Meta:
    model = Journalist 
    fields = "__all__"
 
class ArticleSerializer(serializers.ModelSerializer):

  time_since_publication = serializers.SerializerMethodField()
```
```
class JournalistListCreateAPIView(APIView):
  def get(self.request):
    journalists = Journalist.objects.all()
    serializer = JournalistSerializer(journalists, many =True)
    return Response(serializer.data)
    
  def post(self,request):
    serializer = JournalistSerializer(data=request.data)
    if serialzier.is_valid():
      serializer.save()
      return Response(serializer.data, status = status.HTTP_201_CREATED)
    return Response(serializer.errors, status = status.HTTP_400_BAD_REQUEST)  
```
```
---url.py---
path("journalists/",
    JournalistListCreateAPIView.as_view(),
    name="journalist-list")
```
Json Returns
```
/api/journalists/
[
  {
    ...,
    "articles":[
      {
          "time_since_publicaiton":"16 hours, 54 minutes",
          "first_name":"John",
          "last_name":"Titor",
       },
       {
          "time_since_publicaiton":"16 hours, 54 minutes",
          "first_name":"John",
          "last_name":"Titor",
       }
     ],
     "first_name":"john"
  }
]
```  
Option 4 - Hyperlink sending url for articles\
```
---serializer.py nested serializers---
Class JournalistSerializer(serializers.ModelSerializer):
  articles =serializers.HyperLinkedRelatedField(many=True,read_only=True,view_name="article-detail")
  
  class Meta:
    model = Journalist
    fields = "__all__"
```
```
class JournalistListCreateAPIView(APIView):
  def get(self.request):
    journalists = Journalist.objects.all()
    serializer = JournalistSerializer(journalists, many =True, context = {'request':request})
    return Response(serializer.data)
```
Json Returns
```
/api/journalists/
[
  {
    ...,
    "articles":[
      "http://127.0.0.1:8000/articles/1/",
      "http://127.0.0.1:8000/articles/2/"
     ],
     "first_name":"john"
  }
]
```  
## Notes: Class Based Views. ->Bulk Crud, Single Crud
***
- api/ebook/    (Get Many,Post Many, Put Many, Delete Many , Post Single)
- api/ebook/<int:pk>   (Get Many,Post Many, Put Many, Delete Many , Post Single)
***
```
---- Class Based Views, views.py in api folder----
class EbookListAPIView(APIView):

  def get(self, request):
    ebook= Ebook.objects.all()
    serializer = EbookSerializer(ebook,many=True)
    return Response(serializer.data)

  def post(self,request):
    if type(request.data) is list:
        serializer = EbookSerializer(data = request.data,many=True)   # Create Multiple
    else:
        serializer = EbookSerializer(data = request.data)             # Create Single
    if serializer.is_valid():
        library=Library.objects.first() # Foreign Key
        serializer.save(library=library)
        return Response(serializer.data, status=status.HTTP_201_CREATED)
    return Response(serializer.errors, status.HTTP_400_BAD_REQUEST)

  def put(self, request):
    ebook= Ebook.objects.all()
    serializer = EbookUpdateSerializer(data = request.data,instance=ebook,many=True) #To do: Make sure ids are valid
    if serializer.is_valid():
      serializer.save()
      return Response(serializer.data, status=status.HTTP_201_CREATED)
    return Response(serializer.errors, status.HTTP_400_BAD_REQUEST)
  
  def delete(self,request):
    try:
      ids=(request.data["ids"])
      if type(ids)!=list:
        raise TypeError("ids must be a list")
    except KeyError as e:
      errors=[{str(e): ["This field is required."]}]
      return Response(errors,status.HTTP_400_BAD_REQUEST)
    except TypeError as e:
      errors=[str(e)]
      return Response(errors,status.HTTP_400_BAD_REQUEST)
    except Exception as e:
      errors=["Something Went Wrong"]
      return Response(errors,status.HTTP_400_BAD_REQUEST)    
    ids_not_found=[]
    ids_deleted=[]
    for id in ids:
      try:
        ebook=Ebook.objects.get(pk=id)
        ebook.delete()
        ids_deleted.append(id)
      except Exception as e:
        ids_not_found.append(id)
    res=[{"ids_not_found": ids_not_found,"ids_deleted": ids_deleted}]
    return Response(res,status = status.HTTP_204_NO_CONTENT)

class EbookDetailAPIView(APIView):
  def get_object(self,pk):
    ebook = get_object_or_404(Ebook, pk=pk)
    return ebook
   
  def get(self,request,pk):
    ebook = self.get_object(pk)
    serializer = EbookSerializer(ebook)
    return Response(serializer.data)
   
  def put(self, request, pk):
    ebook =self.get_object(pk)
    serializer = EbookSerializer(ebook, data = request.data)
    if serializer.is_valid():
      serializer.save()
      return Response(serializer.data, status=status.HTTP_201_CREATED)
    return Response(serilizer.errors, status.HTTP_400_BAD_REQUEST)

  def delete(self, request, pk):       #TODO: Handle errors
    ebook=Ebook.objects.get(pk=pk)
    ebook.delete()
    return Response(status = status.HTTP_204_NO_CONTENT)
```
```
---- Serializers, serializers.py in api folder----
class EbookUpdateListSerializer(serializers.ListSerializer):
	def create(self, validated_data):
		ebook = [Ebook(**item) for item in validated_data]
		return Ebook.objects.bulk_create(ebook)
	
	def update(self, instance, validated_data):
        # Maps for id->instance and id->data item.
		eb_mapping = {eb.id: eb for eb in instance}
		data_mapping = {item['id']: item for item in validated_data}

		# Perform creations and updates.
		ret = []
		for eb_id, data in data_mapping.items():
			eb = eb_mapping.get(eb_id, None)
			if eb is None:
				ret.append(self.child.create(data))
			else:
				ret.append(self.child.update(eb, data))
		return ret

class EbookUpdateSerializer(serializers.ModelSerializer):
	id = serializers.IntegerField()

	class Meta:
		list_serializer_class = EbookUpdateListSerializer
		model = Ebook
		fields = ('id','name','description')

class EbookSerializer(serializers.ModelSerializer):

	class Meta:
		model = Ebook
		fields = ('id','title','description')
```
# DRF Level Two
***
- Learn to use the Generic APIView and Mixins Classes
- Learn to use and customize Generic Class Based Views
- Group the results provided by your APIs with a pagination system 
- Secure your Web APIs with a Permissions System
***

## Ebook Example Project
```
-------Models.py---------
from django.db import models
from django.core.valudators import MinValueValidator, MaxValueValidator

class Ebook(models.Model):
  title = models.CharField(max_length=140)
  author = models.CharField(max_length=60)
  description= models.TextField()
  publication_date = models.DateField()
  
class Review(models.Model):
  created_at = models.DateTimeField(auto_now_add=True)
  updated_at = models.DateTimeField(auto_now=True)
  review_author = models.CharField(max_length=8 , blank=True, null=True)
  review = models.TextField(blank=True, null=True)
  rating = models.PositiveIntegerField(validators=[MinValueValidator(1),MaxValueValidator(5)])
  ebook = models.ForeignKey(Ebook, on_delete = models.CASCADE, related_name="reviews")
  
  def __str__(self):
    return str(self.rating)
```
```
-------add serializers.py in api folder---------
from rest_framework import serializers
from ebooks.models import Ebook, Review

class ReviewSerializer(serializers.ModelSerializer):
  class Meta:
    model = Review
    fields="__all__"
    
class EbookSerializer(serializers.ModelSerializer):
  reviews = ReviewSerializer(many=True, read_only=True)
  
  class Meta:
    model = Ebook
    fields="__all__"
    
```
## GenericAPIView & Mixins
***
- One of the key benefits of using the Generic Views in DRF is offers alot of ready-to-use code.
- CRUD operation in a model-backed API will be implemented in the same way in most cases.   
- DRF has a class called GenericAPIView that extends the APIView class.  
    
- GenericAPIView class is often used with Mixins
  - Mixin Classes provide action methods such as .list() or create() rather then defining handler methods such as .get() or .post()
***
https://www.django-rest-framework.org/api-guide/generic-views/#genericapiview . 
```
Basic Attributes :
queryset
serializer_class

Mixin Classes
```
```
----- views.py in api-folder-------
from rest_framework import generics
from rest_framework import mixins

from ebooks.models import Ebook
from ebooks.api.serializers import EbookSerializer

class EbookListCreateAPIView(mixins.ListModelMixin,
                             mixins.CreateModelMixin,
                             generics.GenericAPIView):
                             
    queryset = Ebook.objects.all()
    serializer_class = EbookSerializer
    
    def get(self,request, *args, **kwargs):
      return self.list(request, *args, **kwargs)
    
    def post(self,request,*args, **kwargs):
      return self.create(request, *args, **kwargs)
```
```
----- urls.py --------
from django.urls import path
from ebooks.api.views import EbookListCreateAPIView

urlpatterns = [
  path("ebooks/",EbookListCreateAPIView.as_view(), name ="ebook-list")
]
```
## Concrete View Classes (one of Generic classes thats most practical)
```
class EbookListCreateAPIView(generics.ListCreateAPIView):
  queryset = Ebook.objects.all()
  serializer_class = EbookSerializer
  
class EbookDetailAPIView(generics.RetrieveUpdateDestroyAPIView):
  queryset = Ebook.objects.all()
  serializer_class = EbookSerializer
  
```
```
----- urls.py --------
from django.urls import path
from ebooks.api.views import EbookListCreateAPIView, EbookDetailAPIView

urlpatterns = [
  path("ebooks/",EbookListCreateAPIView.as_view(), name ="ebook-list")
  path("ebooks/",EbookDetailAPIView.as_view(), name ="ebook-detail")
]
```
Dealing with foreign key relationship
```
------views.py-------
from rest_framework.generics import get_object_or_404

class ReviewCreateAPIView(generics.CreateAPIView):
  queryset= Review.objects.all()
  serializer_class = ReviewSerializer
  
  def perform_create(self, serializer):
      ebook_pk = self.kwargs.get("ebook_pk")
      ebook = get_object_or_404(Ebook, pk=ebook_pk)
      serializer.save(ebook=ebook)      //changing the specific ebook instance to be saved

class ReviewDetailAPIView(generics.RetriveUpdateDestroyAPIView):
  queryset= Review.objects.all()
  serializer_class = ReviewSerializer
```
```
----serializers.py--------
# Remove the ebook instance from serializer
class ReviewSerializer(serializers.ModelSerializer):
  class Meta:
    model = Review
    exclude = ("ebook",)
```
```
----urls.py-----
from django.urls import path
from ebooks.api.views import EbookDetailAPIView, EbookListCreateAPIView, ReviewCreateAPIView, ReviewDetailAPIView

urlpatterns = [
  path("ebooks/",EbookListCreateAPIView.as_view(), name ="ebook-list"),
  path("ebooks/<int:pk>",EbookDetailAPIView.as_view(), name ="ebook-detail"),
  path("ebooks/<int:ebook_pk>/review/",ReviewCreateAPIView.as_view(), name ="ebook-review"),
  path("reviews/<int: pk>/",ReviewDetailAPIView.as_view(), name ="review-detail")
]
```
## The Permissions Systems Part One
https://www.django-rest-framework.org/api-guide/permissions/ . 
  
```
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ]
}

// If not specificed Defauts to 
'DEFAULT_PERMISSION_CLASSES': [
   'rest_framework.permissions.AllowAny',
]

'DEFAULT_PERMISSION_CLASSES': [
   'rest_framework.permissions.IsAuthenticatedOrReadOnly',
]

```
  
When Not Authenticated returns . 
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/drf-vue1.png)   
  
### Setting permissions per api 
```
---views.py in api folder---------
class EbookListCreateAPIView(generics.ListCreateAPIView):
  queryset = Ebook.objects.all()
  serializer_class = EbookSerializer
  permission_classes = [permissions.IsAutheticatedOrReadOnly]
```
### Including auth 
```
---urls.py---
urlpatterns = [
  path('api-auth/',include("rest_framework.urls")),
]
```
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/drf-vue2.png)   
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/drf-vue3.png)   
  
Creating ur own permission class
```
--- permission.py in api folder-----
from rest_framework import permissions

class IsAdminUserOrReadOnly(permissions.IsAdminUser):
  
  def has_permission(self,request,view):
    is_admin = super().has_permission(request,view)
    return request.method in permissions.SAFE_METHODS or is_admin

```
Using custom permission class in views.py
```
--- views.py in api folder---
from rest_framework import permissions

class EbookListCreateAPIView(generics.ListCreateAPIView):
  queryset = Ebook.objects.all()
  serializer_class = EbookSerializer
  permission_classes = [permissions.IsAdminUserOrReadOnly]
```

## The Permissions Systems Part Two
secure our review instances so taht they can be updated or deleted only by the same users who have created them.   
  
In order to do so we will first need to modify our Review model, binding it to Django's User model using a ForeignKey field.  
```
----models.py----- #Adding reviews to User-Author
from django.contrib.auth.models import User

class Review(models.Model):
  review_author= models.ForeignKey(User, on_delete = models.CASCADE)
```

```
----serializers.py---- 
class ReviewSerializer(serializers.ModelSerializer):
  review_author = serializers.StringRelatedField(read_only=True)
  
  class Meta: 
    model = Review
```

```
----views.py----
class ReviewCreateAPIView(generics.CreateAPIView):
  queryset = Review.objects.all()
  serializer_class = ReviewSerializer
  permission_classes = [permissions.IsAutheticatedOrReadOnly]
  
  def perform_create(self,serializer):
    review_author = self.request.user
    
    review_queryset = Review.objects.filter(review_author=review_author) . # make sure one review <->one ebook
    if review_queryset.exists():
      raise ValidationError("You have already reviewed this book!)
    
    serializer.save(review_author=review_author)
```
### Adding Permission class to allow review author to edit their own review
```
----permissions.py------
class IsReviewAuthorOrReadOnly(permissions.BasePermission):
  def has_object_[permission(self,request,view,obj):
    if request.method in permissions.SAFE_METHODS:
      return True
      
    return obj.review_author == request.user
```
```
---views.py----
class ReviewDetailAPIView(generics.RetrieveUpdateDestroyAPIView):
  ...
  permission_classes = [IsReviewAuthorOrReadOnly] // add custom permissions into views
```
## Pagination System 
django-rest-framework.org/api-guide/pagination/   
  
**Request**  
```
GET https://api.example.org/accounts/?page=4
```
**Response**   
```
HTTP 200 OK
{
  "count":1023,
  "next":"https://api.example.org/accounts/?page=5",
  "previous":"https://api.example.org/accounts/?page=3",
  "results":[
    ...
  ]
}
```
### Setting pagination globally
```
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.LimitOffsetPagination',
    'PAGE_SIZE': 100
}
```
### Setting pagination per view 
```
---create pagination.py in api folder----
from rest_framework.pagination import PageNumberPagination

class SmallSetPagination(PageNumberPagination):
  page_size = 3
```
```
--- views.py-----
from ebooks.api.pagination import SmallSetPagination

class EbookListCreateAPIView(generics.ListCreateAPIView):
  queryset = Ebook.objects.all().order_by("-id") //order ur queryset to order properly
  serializer_class = EbookSerializer
  permission_classes = [IsAdminUserOrReadOnly]
  pagination_class = SmallSetPagination
```
![Image](https://github.com/KennySoh/Technical-Interview/blob/master/oop/drf-vue4.png) 

# DRF Level Three
***
- Knowledge of the main Authentication Methods in DRF
- Set Up a Registration and Authentication System via REST
- Familiarity with Django-REST-Auth
- Knowledge of Viewset and Router Classes
- Filtering via Django REST Framework
- Being able to write automated tests with Django and DRF

- Bonus: how to extend Django's User Model with a custom Profile Model
***
## UserProfiles API
***
- Extend Django basic User model with a second model
- Store further information about our users such as a user's biography, city and avatar.
- Each user will then be able to write status messages that will be bind to his profile

- Django Signals, allow certain senders to notify a set of receivers that some action has taken place elsewhere in the framework
- Automatically create and bind a Profile's Instance to a User Object as soon as new one is created
***
### Setup
```
------settings.py------
INSTALLED_APPS=[
  ...
  'rest_framework',
  'profiles'
]

MEDIA_URL="/media/"
MEDIA_ROOT="uploads"
```
```
-----urls.py----
if settins.DEBUG:
  urlpatterns += static(settings.MEDIA_URL, document_root = settings.MEDIA_ROOT)
```
### Creating the Models
bind user model to profile model 
```
from django.db import models
form django.contrib.auth.models import User

class Profile(models.Model):
  user = models.OneToOneField(User, on_delete = models.CASCADE)
  bio = models.CharField(max_length = 240 , blank = True)
  city = models.CharField(max_length = 30 , blank = True)
  avatar = modelsImageField(null=True, blank = True)
  
  def __str__(self):
    return self.user.username
    
class ProfileStatus(models.Model):
  user_profile = models.ForeignKey(Profile, on_delete = models.CASCADE)
  status_content = models.CharField(max_length = 240)
  created_at = models.DateTimeField(auto_now_add = True)
  updated_at = models.DateTimeField(auto_now = True)
  
  def __str__(self):
    return str(self.user_profile)
```
## UserProfilesAPI - Project Setup Part Two
Send a signal everytime a user is saved,   
a function with decorator receiver will receive the signal  
- we will know if user has been created or modified
```
---- signals.py-----
from django.contrib.auth.models import User
from django.db.models.signals import post_save
from django.dispatch import receiver
from profiles.models import Profile

@receiver(post_save, sender = User)
def create_profile(sender , instance, created, **kwargs):
  print("Created: ", created)
  if created:                               # if user has just been created=True, create a profile instance
    Profile.objects.create(user=instance)
  
```
CONFIGURATIONS
```
----apps.py----
from django.apps import AppConfig

class ProfileConfig(AppConfig):
  name='profiles'
  
  def ready(self):
    import profiles.signals
```
### Create API Serializer
```
---- serializers.py in api folder----
from rest_framework import serializers
form profiles.models import Profile, ProfileStatus

class ProfileSerializer(serializers.ModelSerializer):
  user = serializers.StringRelatedField(read_only = True)
  avatar = serializers.ImageField(read_only = True) #Create another end point to update media individually
  
  class Meta:
    model = Profile
    fields = "__all__"

class ProfileAvatarSerializer(serializers.ModelSerializer):     #only update media avatar for one endpoint
  class Meta:
    model = Profile
    fields = ("avatar",)

class ProfileStatusSerializer(serializers.ModelSerializer):
  user_profile = serializers.StringRelatedField(read_only=True)
  
  class Meta:
    model = ProfileStatus
    fields = "__all__"
```
## Authetication
Associate a series of identification credentials to an incoming request, obtaining critical information such as the specific user  
  
We can then user a system of permissions to decide wether or not to accept the incoming request  based on the type of users( admin users, basic users and so on..)  
  
### Basic Authetication 
Most Primitive and least secure. Only for testing. 

***
Request/Response cycle
-> The client makes a HTTP request to the server
<- The server responds with a HTTP 401 Unauthorized response containg the WWW-AUthenticate header, explaining how to autheticate(WWW-Authenticate:Basic)
-> The Client sends it authcredentials in base 64 with the Authorization header.
Authentication credentials are here unencrypted.
<- The server evaluates the access credentials and responds with the 200 or 403 status code, therefore authorizing or denying the client's request.
***
### Token Authentication 
This is the ideal system for authenticating smartphone and desktop clients.  
  
Authentication token gets saved either in a cookie or in the browser's localStorage. 
... authentication token in localStorage is very dangerous, as it makes it vulnerable to XSS attacks!  
  
Using a httpOnly cookie on the other hand is much safer because this way the token cant be accessed via Javascript... but because of the you are now losing the flexibility that you would get by using localStorage instead!  
***
Request/Response cycle
-> The client sends it's authentication credentials once
<- The server checks the credentials, and if they are valid it creates an exclusive signed token made of a string of characters that then sends back to the client as response
-> The Client sends its token with the Authorization Header of every following request
<- The server checks the received token and if valid, allows the request to proceed.
***

It is the authentication scheme that we will use in the Final Project. 
  
If successfully autheticated using Session Authetication, Django will provide us the corresponding User Object, accessible via request.user  
  
For non-authenticated requests, an AnonymousUser instance will be provided instead.
  
**Important** Once the authticated via session auth, the framework will require a valid CSRF token to be sent for any unsafe HTTP method request such as PUT, PATCH, POST, DELETE. 
### Session Authetication
This authentication scheme uses Django's default session backend for authentication.  
  
Session authetication is the safest and most appropriate way for authenticating AJAX clients that are running in the same session context as your website, and uses a combination of Sessions and Cookies. 
***
Request/Response cycle
-> Users send their authetication credentials, typically using a Login Form
<- Server checks the data and if correct, it creates a corresponding Session Object that will be saved in the database, sending back to the client a Session ID
-> The Session ID gets saved in a Cookie in the browser and will be part of every future request to the server, that will check it every time
-> when the client logs out, the Session ID is destroyed by both the client and the server, and a new one will be created at the next login
***

### Bonus JWT
One of the main differences with other token-based standards is that because of their structure JWT tokens dont require database validation.  
  
JSON Web tokens can be easily used in a DRF powered REST API using the django-rest-framework-simplejwt package.  
  
## Django-REST-Auth Part1
In this lesson you will learn how to use the Django-REST-Auth package in order to expose registration and authentication endpoints for your REST APIs!  
  
Thanks to these endpoints, clients such as Androis and iOS apps will be able to easily and indepndently communicate with all the services provided by your web app's backend via REST.
### Setting authetication globally
https://www.django-rest-framework.org/api-guide/authentication/
```
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        # 'rest_framework.authentication.BasicAuthentication', #Can comment out for testing
        'rest_framework.authentication.SessionAuthentication',
	'rest_framework.authentication.TokenAuthentication
    ]
}

INSTALLED_APPS = [
    ...
    'rest_framework.authtoken'
]
```

### install django-rest-auth
Django-rest-auth library provides a set of REST API endpoints for registration, authentication (including social media authentication), password reset, retrieve and update user details, etc. By having these API endpoints, your client apps such as AngularJS, iOS, Android, and others can communicate to your Django backend site independently via REST APIs for user management.
```
pip install django-rest-auth
```
```
---settings.py-----
INSTALLED_APPS = [
    ...
    'rest_auth'
]
```
```
---urls.py---
urlpatterns=[
	path("api-auth/",include("rest_framework.urls")),
	path("api/rest-auth/",include("rest_auth.urls"))
]
```
  
#### rest-auth.views import LoginView
***
- Accept the following POST parameters:username, password
- Return the REST Framework Token Object's key. 
***
Using the end point
```
import requests

def client():
	credentials ={"username":"admin","password":"asdasdasd"}
	response = request.post("http://127.0.0.1:8000/api/rest-auth/login/",
				data=credentials)
	print("Status Code: ", response.status_code)
	response_data = response.json()
	print(response_data)
if __name__=="__main__":
	client()

-------
returns  Status Code: 200 {'key':'affe53j20vvbF345j295j3290k1k2kko1ju21'}
```
### Is Authenticated permissions for Views
```
-----views.py----
from rest_framework import generics
from rest_framework.permissions import IsAuthenticated
from profiles.models import Profile
from profiles.api.serializers import ProfileSerializer

class ProfileList(generics.ListAPIView):
	queryset = Profile.objects.all()
	serializer_class = ProfileSerializer
	permission_classes = [IsAuthenticated]
```

Including Token in request
```
import requests

def client():
	token_h = "Token affe53j20vvbF345j295j3290k1k2kko1ju21"
	headers = {"Authorization":token_h}
	
	response = request.get("http://127.0.0.1:8000/api/api/profiles/",
				headers=headers)
	print("Status Code: ", response.status_code)
	response_data = response.json()
	print(response_data)
if __name__=="__main__":
	client()

```
## Django-REST-Auth Part2 
Setup registrations end point so users can create new account via rest

```
pip install django-allauth   	#Dependecy of django rest auth
pip freeze > requirement.txt
```

```
---settings.py---
INSTALLED_APPS = [
	...
	'django.contrib.sites',
	
	'allauth',
	'allauth.account',
	'allauth.socialaccount',
		
	'rest_auth',
	'rest_auth.registration'
]

...End of file
SITE_ID =1
ACCOUNT_EMAIL_VERICATION = "none"
ACCOUNT_EMAIL_REQUIRED = (True)
```
```
---urls.py----
urlpatterns = [
	path("api/rest-auth/registration/", include("rest_auth.registration.urls"))
]
```

Sending a client registration to end point
Including Token in request
```
import requests

def client():
	data={
		"username":"admin",
		"email":"test@rest.com",
		"password1":"asdasd",
		"password2":"asdasd"
	}
	
	response = request.get("http://127.0.0.1:8000/api/rest-auth/registration",
				data=data)
	print("Status Code: ", response.status_code)
	response_data = response.json()
	print(response_data)
if __name__=="__main__":
	client()

Returns Status Code: 2-1 ,{'key','640c2db23d832af832g8h239dcgrvvd28329'}
```

## ViewSets & Routers
***
ViewSet classes allow us to combine the logic for a set of related views in a single class : 
- Get a list of elments from a queryset
- get the details of a single instance of the same model

- Highest abstraction level
***
  
They are another kind of Class Based View, that does not provide any method handlers such as .get() or .post() but instead provide action methods such as **.list()** and **.create()**.  
    
**Commonly used with Router** . 

### Adding Viewsets
```
----views.py in api folder----
...
from rest_framework.viewsets import ReadOnlyModelViewSet 

class ProfileViewSet(ReadOnlyModelViewSet):
  queryset = Profile.objects.all()
  serializer_class = ProfileSerializer
  permission_classes = [IsAuthenticated]
```
```
----urls.py---
from django.urls import path
from profiles.api.views import ProfileViewSet

profile_list = ProfileViewSet.as_view({"get":"list"})
profile_detail = ProfileViewSet.as_view({"get":"retrieve"})

urlpatterns = [
	path("profiles/",profile_list. name="profile-list"),
	path("profiles/<int:pk>/", profile_detail, name="profile-detail"),
]
```
### Adding Router
use the router class to automatically create the endpoints from Viewsets
```
----urls.py---
from django.urls import include, path
from rest_frameworks.routers import DefaultRouter
from profiles.api.views import ProfileViewSet

router = DefaultRouter()
router.register(r"profiles", ProfileViewSet)

urlpatterns = [
	path("",include(router.urls))
]
```

This results in API ROOT, API list,API detail

# Vue Js
## Introduction
### A Progressive Framework:
Application Complexity vs Framework Complexity ....  
- Will feel guilty using angular to build a static page vs vanila javascript to build gmail  
### Vue Ecosystem
The Vue ecosystem is formed by a series of complementary official projects, which allow us to extend its capabilities far beyond the "core view layer" according to our needs:
***
- Vue-Router (Single Page Application Routing)
- VueX(Large Scale State Management)
- Vue-CLI (Project Scaffolding - Rapid Development Toolkit)
- Vue-Loader (Single File Component(*.vue file) loader for web pack)
- Vue-DevTools (Browser DevTool Extension)
- Vue-Server-Renderer
- Vue-Class-Component
- Vue RXs
***

## First Vue Instance
***
- Create vue folder
- Create veu.html
- visual studio>html5 for boiler plate code
- copy path 
***
### Including vue.js 

We import via CDN for this . 
https://vuejs.org/v2/guide/installation.html <- we can also install via npm 
```
---vue.html---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Hello Vue</title>
</head>
<body>
	<div id="app"></div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>
	<script src="yourmain.js">
</body>
</html>
```
### Creating a new vue instance
```
---yourmain.js---
var app = new Vue({
	el: '#app',    			//el expects a css selector
	data:{					//all the variable
		message:"Hello world!",
		value:5
		imgSrc: "https://cdn.pixabay.com/photo/1234.jpg"
	}
})
```
```
---vue.html---
...
<div id=app>
	<h1>{{ message }}</h1> 		//Commonly used this
	<h1 v-text="message"></h1>
	
	<h2>{{ value * 5 }}</h2>
	<h2>{{ "Hello" + " Vue!" }}</h2>
	<h2>{{ (33/11) * 5 }}</h2>
	<h2>{{ Math.random() }}</h2>
	<h2>{{ message.split('').reverse().join('') }}</h2>
	
	<img v-bind:src="imgSrc" alt=""></h2>
	<a v-bind:href = "link">Official Websites</a>
</div>
```
## Events and Methods
Let our Vue Application listen for DOM events that we can use to trigger different methods defined in the application itself.   
  
Introduce the **v-on directive**
  
```
var app= new Vue({
	el:'#app',
	data:{
		lesson:"Events and Methods",
		counter:0
	},
	methods:{
		incrementCounter(){
			this.counter+=1;
			console.log(this.counter);
			if(this.counter === 10){
				alert("Counter is at 10!");
		},
		overTheBox(){
			console.log("Over the green box")
		}
	}
})
```
```
---vue.html---
...
<h1>{{ lesson }}</h1>
<h3>Counter: {{ counter }}</h3>
<button v-on:click="counter += 1">Increment ++</button>
<button v-on:click="incrementCounter += 1">Increment ++</button>

<div class="box" @mouseover=="overTheBox"></div>
```
## Conditional Rendering 
**v-if , v-else**  
```
var app= new Vue({
	el:'#app',
	data:{
		auth:false,
		product:"Sunglasses",
		quantity:0,
		sale:true
	},
	methods:{
		incrementCounter(){
			this.counter+=1;
			console.log(this.counter);
			if(this.counter === 10){
				alert("Counter is at 10!");
		},
		overTheBox(){
			console.log("Over the green box")
		}
	}
})
```
```
---vue.html---
<div id="app">
	<h1 v-if="auth"> Your User Profile </h1>
	<h1 v-else>Login to Access Your Profile!</h1>
	
	<h1> Product: {{ product }}
	<h2 v-if="quantity >= 20"> Available </h1>
	<h2 v-else-if="quantity > 0 && quantity < 20">Limited Availability</h1>
	<h2 v-else>Sold Out</h2>
	<br>
	<h3 v-show="sale">On Sale!!!!</h3>
</div>
```
js console   
-> app.auth = true   
-> app.auth = false 
  
-> app.quantity=20  
-> app.sale = true  

## Class & Style Binding 
**v-bind**
```
var app= new Vue({
	el:'#app',
	data:{
		flag:false,
		styleObject:{
			backgroundColor: 'green',
			border: '5px solid orange'
		}
	},
	methods:{
		changeShape(){
			this.flag = !this.flag;
		}
	}
})
```
```
 ----vue.html----
 <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min/css">
 <style> 
 	.circle{
		width: 250px;
		height:250px;
		border-radius:50%;
	}
	.square{
		width: 250px;
		height:250px;
	}
</style>
<body>
	<div id="app">
		<div class = "row justify-content-center mt-3">
			<div v-bind:class="{ circle:flag, square:!flag }" v-bind:style="styleObject"></div>
		</div>
		<div class = "row justify-content-center mt-3">
			<button class="btn btn-success" @click="changeShape">Change Shape</button>
		</div>
	</div>
	...
</body>
```
## List Rendering with v-for
**v-for** 
```
---main.js---
var app = new Vue({
	el:"#app",
	data: {
		users: [{
			id:567,
			name:"alice",
			profession:"developer"
		},{
			id:568,
			name:"kenny",
			profession:"developer"
		},{
			id:568,
			name:"jack",
			profession:"marketer"
		}]
	}
})
```
```
---.html---
<div id="app">
	<h1>Users List</h1>
	<div class="card" v-for="user in users" :key="user.id">
		<div class="card-body">
			<p><strong>Name:</strong> {{ user.name }}</p>
			<p><strong>Professsion:</strong> {{ user.profession }}</p>
		</div>
	</div>
</div>
```
## Computed Properties
Its possible to define and use expression directly within our templates: (not reccomended) . 
```
<h1> {{ (33/11)*5 </h1>
```

A better alternative is to use the computed values. Can be think of extension of our data model.
```
var app = new Vue({
	el:"#app",
	data:{
		first_name: "John",
		last_name:"Doe"
	}
	computed: {
		getRandomComputed(){ 			//similar to a value 
			return Math.random()
		},
		fullName(){
			return `${ this.first_name } ${ this.last_name }
		},
	},
	methods:{
		getRandomNumber(){
			return Math.random();
		}
	}
})
```
```
<p>Method -1: {{ getRandomNumber() }} </p>
<p>Method -1: {{ getRandomNumber() }} </p>

<p>Computed -1: {{ getRandomComputed }} </p>
<p>Computed -1: {{ getRandomComputed }} </p>

<p> {{ fullName }} </p>
```
computed: vs methods:

## Forms and User Input
```
--allow us to create a 2 way binding ---
immediate reflects changes accordingly 


```
v-model chnges data immediately

- validation 

## Components and Props 
```
Vue.component("comment",{

}
```
## How to use  $emit
we are going to make a child component communicate with its parent using $emit, giving them the ability to call methods an pass values.. altering the prop memory
```
// List Component - Parent

// Single Comment component -single 
```

# Final Project 
## Intro- Vue.js, Django Spa
***
- How to use Django, DRF and Vue Js to build Real World Projects
- How to use Vue CLI and Vue Router
- How to build Single PageApplications with Vue JS and Vue CLI
- How to keep Webpack's Hot-Module-Replacement (HMR) working with VueCli and Django during development
- How to use session authenticaiton in a DRF powered SPA
***
### Users Application and Authentication Settings
- AbstractUser
- 
### User Authentication - Settings and Templates 
### Single Page Application Entry-Point and First REST Endpoint 
### Models and Signals
### Serializers
### Question ViewSet
### Creation and Listing
### Authentication Template - CSS Styling 
### Vue CLI, Node and Single Page Applications
### 
