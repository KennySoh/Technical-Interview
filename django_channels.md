# Django Channels 
Websockets, ASGI, Channels
https://www.youtube.com/watch?v=F4nwRQPXD8w

## Websockets
***
- Bi-directional protcol 
- Full duplex communication 
-- client and server can talk at the same time
***

![Screenshot 2021-08-27 at 3 50 36 PM](https://user-images.githubusercontent.com/32699647/131092479-27732f56-29d7-4577-a3d0-5c51452cce43.png)

## Async and Await
https://www.youtube.com/watch?v=bs9tlDFWWdQ
- Acheieving concurrency in python. 
- MultiThreading

## Django Channels
***
How do we know who to send the messsage to? by using channels.
- Every client has a reply_channel
- Keep track of user in a connected list
- chat app -> multiple users ( one room)
- Channels uses groups 
***
![Screenshot 2021-08-27 at 3 55 51 PM](https://user-images.githubusercontent.com/32699647/131093214-45161e4e-d744-410c-a301-709dca753177.png)

### Consumers
- Consumers are like Django views.
- Routing are like Django urls. (Decides which consumer should be called on incoming requests)
- Long running except for Http events

### Routing 
- Routers - Protocol

### Cross Process Communication 
- Each user will have serperate socket connection( application instance)
- In group chat received message can be send to other sockets/application instances
- Can be neabled using channel layer 

### Installation
***
- Install Django Channels
- Create Django Templates / Views
- Channels Routing
- Consumer (view)
- Template configuration handle WS
***
```
python -m venv venv
venv/bin/activate

pip install django

# -- https://channels.readthedocs.io/en/stable/installation.html --
# 1) Install Django Channels
python -m pip install -U channels

# 2) Include channels in Installed APP

INSTALLED_APPS = (
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.sites',
    ...
    'channels',
)

# 3) asgi.py

import os

from channels.routing import ProtocolTypeRouter
from django.core.asgi import get_asgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'django_channels.settings')

application = ProtocolTypeRouter({
    "http": get_asgi_application(),
    # Just HTTP for now. (We can add other protocols later.)
})

# 4) Set ASGI Application
ASGI_APPLICATION = "core.routing.application"
```

### Routing 
- Routers - Protocol

``` 
-- mainapp core.routing.py -----
from channels.auth import AuthMiddlewareStack # Use django authentication (Not-compulsory)
from channels.routing import ProtocolTypeRouter, URLRouter
#import chat.routing

application = ProtocolTypeRouter({
  'websocjet':AuthmiddlewareStack(
    URLRouter(
      chat.routing.websocket_urlpatterns
      # application.routing.websocket_urlpatterns
    )
  ),
})
```

``` 
-- sideapp chat.routing.py -----
from django.urls import re_path

websocket_urlpatterns = [
  re_path(r'ws/chat/(?P<room_name>\w+)/$' , consumers.ChatRoomConsumer),
]
```

### Consumers
- Consumers are like Django views.
- Routing are like Django urls. (Decides which consumer should be called on incoming requests)
- Long running except for Http events

https://channels.readthedocs.io/en/stable/topics/consumers.html#channel-layers

``` 
-- sideapp chat.consumer.py -----
from channels.generic.websocket import AsyncWebsocketConsumer

class ChatRoomConsumer(AsyncWebsocketConsumer):
    async def connect(self):
        self.room_name = self.scope['url_route']['kwargs']['room_name']
        self.room_group_name = 'chat_%s' % self.room_name
        
        await self.channel_layer.group_add(
            self.room_group_name,
            self.channel_name
        )
        
        await self.accept() // To accept incoming connection
        
        await self.channel_layer.group_send(
            self.room_group_name,
            {
                'type': 'tester_message',
                'tester': 'hello_world',
            }
        )
        
    async def tester_message(self, event):
        tester = event['tester']
        
        await self.send(text_data = json.dumps({
            'tester':tester,
        }))
        
    async def disconnect(self, close_code):
        await self.channel_layer.group_discard(
            self.room_group_name,
            self.channel_name
        )
    
    //receiving data
    async def receive(se;f,text_data):
        text_data_json = json.loads(text_data)
        message = text_data_json['message']
        
        await self.channel_layer.group_send(
            self.room_group_name,
            {
                'type':'chatroom_message',
                'message':message,
            }
        )
   
   async def chatroom_message(self,event):
        message = event['message']
        
        await self.send(text_data=json.dumps({
            'message' : message, 
        }))
        
   pass

### Channel Layer using an inMemory
```
-- In production u have to use redis ---

-- just to get up and running ---
CHANNEL_LAYERS = {
    "default": {
        "BACKEND": "channels.layers.InMemoryChannelLayer"
    }
}
```

### Frontend calling websocket
```js
<script>
    const chatSocket = new WebSocket(
        'ws://'+
        window.location.host + #127.0.1.0:8002 
        '/ws/chat/' +
        roomName +
        '/'
    );
    
    chatSocket.onmessage = function (e){
        const data = JSON.parse(e.data);
        console.log(data)
    }
    
    //sending Data
    chatSocket.send(JSON.stringify({
        'message':message,
    }));
    
    
</script>
```
