# Nest.js 
## Creating a controller
```
import { Controller, Get } from '@nestjs/common'

@Controller()
export class AppController{
  @Get()
  getRootRoute(){
    return 'Hi there, getRootRoute function will run.'    
  }
}
```
Routing decorator
```
/app/product
/app/bye

@Controller('/app')
export class AppController{
  @Get('/product')
  getRootRoute(){
    return 'product'    
  }
  @Get('/bye')
  getRootRoute(){
    return 'bye'    
  }
}
```

## Creating a Module
```
import {Module} from '@nestjs/common'
import {AppController} from ./app.controller.js
import { NestFactory } from '@nestjs/core'

@Module({
  controller: [AppController]
})
class AppModule{}

async function bootstrap(){
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

## File naming convention
```
app.controller.ts
class AppController

app.module.ts
class AppModule
```

## Using the nest cli
```
sudo npm install -g @nestjs/cli
nest new <project-name>
```

<img width="713" alt="Screenshot 2021-09-21 at 9 16 23 AM" src="https://user-images.githubusercontent.com/32699647/134097680-adc26046-3079-452a-9f6f-2f823ced19fa.png">
