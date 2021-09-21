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
<img width="713" alt="Screenshot 2021-09-21 at 9 16 23 AM" src="https://user-images.githubusercontent.com/32699647/134097680-adc26046-3079-452a-9f6f-2f823ced19fa.png">
  
taking away guard , cause this app doesnt have authentication and modules wrap all the components.
<img width="1036" alt="Screenshot 2021-09-21 at 9 23 31 AM" src="https://user-images.githubusercontent.com/32699647/134098272-18408561-63c7-480e-b433-8e5a2ae0f8e4.png">

```
sudo npm install -g @nestjs/cli
nest new <project-name>

npm run start:dev
// disable eslintrc, you can comment out eslintrc.js
```
## Generating files from scratch
```
nest generate module message
nest generate controller messages/messages --flat //watch tutorial for more info
```

## Adding Routing Logic
```
@Controller('/messages')
export class Messages Controller{
  @Get()
  listMessages(){
  }
  
  @Post()
  createMessage(){
  }
  
  @Get('/:id')
  getMessage(){
  }
}
```
- Use Postman to test your routes. 
- VSCode REST Client Extension

## Accessing Request Data with Decorators in controller
<img width="701" alt="Screenshot 2021-09-21 at 10 16 44 AM" src="https://user-images.githubusercontent.com/32699647/134101819-881a8595-6b26-4bc9-b9d6-955f33a52b0a.png">
  
```
import {}

@Controller('/messages')
export class Messages Controller{
  @Get()
  listMessages(){
  }
  
  @Post()
  createMessage(@Body() body:any){
    console.log(body);
  }
  
  @Get('/:id')
  getMessage(@Param('id' id:string){
    console.log(id);
  }
}
```

## Using Pipes for Validation, Adding Validation Rules
***
1. Tell Nest to use Global Validation
2. Create a class that describes the different properties that the request body should have Data transfer object . Dto
3. Add Validation rules to the class
4. Apply that class to the request handler
***
  
**Step1: Tell Nest to use Global Validation**. 
```
-- main.ts--
import {ValidationPipe } from '@nestjs/common'

app.useGlobalPipes(
  new ValidationPipe()
); 
```
  
**Step2: Create a class that describes the different properties that the request body should have Data transfer object . Dto**
```
-- src>messages>dtos>create-message.dto.ts
export class CreateMessageDto {
  content: string;
}
```
**step3: Add Validation rules to the class**. 
add class-validator library. 
```
npm install class-validator class-transformer. 
```
```
import { IsString } from 'class-validator';

export class CreateMessageDto{
  @IsString()
  content:string;
}
```
  
**step4: Apply that class to the request handler**
```
import { CreateMessageDTO } from './dtos.create-message.dto.ts


```

