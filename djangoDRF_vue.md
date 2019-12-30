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
