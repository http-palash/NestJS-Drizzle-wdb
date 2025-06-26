npm install -g nestjs/cli

OR 

npm install -g nestjs/cli@latest
nest new nestjs-drizzle 
choose pnpm as package manager 

npm install @nestjs/common @nestjs/core

Exploring structure :

## src directory >

1. **main.ts>**
- Entry point of application 
- We calling here **bootstrap function** which is creating our application using **app module**
- Exposing traffic on **port 3000** by calling app.listen(3000) to **start our express http server** to start **listening for http connection** [means we can now perform http operation here at this endpoint]

- **app.module.ts >** AppModule
- Here we intialized AppController [app.controller.ts] as controller and AppService [app.service.ts] as provider 
- **provider** : that we can inject into other provider in our application 
- **appcontroller as controller** here is entry point for the http traffic


- **app.controller.ts >** 
- @Controller decorators which is marks it as a  @Controller 
- We can notice we are also **injecting appService in this controller** using constructor of class AppService

- Here we find a single **@Get route which is exposing getHello()** function 
- appService instance here is used to call this getHello


- **app.service.ts >**
- We can see in AppService class we have getHello() function where we are returning a string 
- As we marked this service as provider so it comes with providers capabilities i.e we can  
- And we marked this provider as a injectible decorator [which means we can inject it into other NestJS classes using dependency injection]

All providers and controllers are wired up in app.module which is bootstrap by our bootstrap function

Starting project :

package.json 

scripts{
    "start:dev":"nest start --watch" # watch mode to automatically look changes to our code when we recompile it 
}

Enable-WindowsOptionalFeature -Online -FeatureName $("Microsoft-Hyper-V", "Containers") -All

wsl --install
wsl --list --verbose
docker-compose up --build


setting up docker compose file to use postgress container 

installing pgadmin 4
https://www.postgresql.org/ftp/pgadmin/pgadmin4/v9.4/windows/


pg admin to connect to postgres conatiner running on machine 

https://orm.drizzle.team/docs/get-started/postgresql-new

register servel here with name Local and db localhost at 5432 port [docker container] password example


pnpm add drizzle-orm pg 

pnpm add -D drizzle-kit @types/pg

pnpm i @nestjs/config 
used to inject env variables in application through document library which nest js use under the hood 