# Django Channels 
Websockets, ASGI, Channels

## Websockets
***
- Bi-directional protcol 
- Full duplex communication 
-- client and server can talk at the same time
***

![Screenshot 2021-08-27 at 3 50 36 PM](https://user-images.githubusercontent.com/32699647/131092479-27732f56-29d7-4577-a3d0-5c51452cce43.png)

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


