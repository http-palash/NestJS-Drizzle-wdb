NestJS + Drizzle ORM + PostgreSQL Setup Guide
Overview
This guide walks you through setting up a NestJS project integrated with Drizzle ORM and PostgreSQL, including Docker setup and useful commands to get started quickly.

Prerequisites
Node.js & npm installed

pnpm installed (preferred package manager)

Docker & WSL (for Windows users)

PostgreSQL (via Docker container)

pgAdmin 4 (optional, for managing PostgreSQL visually)

Step 1: Install NestJS CLI
bash
Copy
Edit
npm install -g @nestjs/cli
# OR install latest version explicitly
npm install -g @nestjs/cli@latest
Step 2: Create a new NestJS project
bash
Copy
Edit
nest new nestjs-drizzle
Choose pnpm as the package manager when prompted

Step 3: Install core NestJS dependencies
bash
Copy
Edit
pnpm add @nestjs/common @nestjs/core
Step 4: Project structure overview (src/ directory)
main.ts

Entry point of the application

Contains the bootstrap() function which creates the app using AppModule

Starts the HTTP server on port 3000: app.listen(3000)

This is where HTTP traffic is accepted

app.module.ts

Root module where application components are wired

Registers AppController as a controller and AppService as a provider

Providers are injectable services available throughout the app

Controllers handle incoming HTTP requests

app.controller.ts

Decorated with @Controller(), marking it as a controller

Injects AppService via constructor dependency injection

Defines a simple @Get() route exposing the getHello() method

app.service.ts

Marked as a provider with @Injectable()

Contains business logic, here the getHello() method that returns a greeting string

Can be injected into other components via DI

Step 5: Running the project in development mode
In your package.json, add the following script:

json
Copy
Edit
"scripts": {
  "start:dev": "nest start --watch"
}
This runs the app in watch mode, recompiling on code changes

Run:

bash
Copy
Edit
pnpm run start:dev
Step 6: Setup Docker and PostgreSQL
Enable Windows features for Docker (Windows only)
powershell
Copy
Edit
Enable-WindowsOptionalFeature -Online -FeatureName $("Microsoft-Hyper-V", "Containers") -All
Install and configure WSL
bash
Copy
Edit
wsl --install
wsl --list --verbose
Start Docker Compose with PostgreSQL container
Create a docker-compose.yml file with PostgreSQL configuration and then run:

bash
Copy
Edit
docker-compose up --build
Step 7: Install and configure pgAdmin 4
Download pgAdmin 4 for Windows:

https://www.postgresql.org/ftp/pgadmin/pgadmin4/v9.4/windows/

Use pgAdmin to connect to your running PostgreSQL container:

Register a new server

Name: Local

Host: localhost

Port: 5432

Password: your container password

Step 8: Install Drizzle ORM and dependencies
bash
Copy
Edit
pnpm add drizzle-orm pg
pnpm add -D drizzle-kit @types/pg
Step 9: Load environment variables with NestJS Config Module
bash
Copy
Edit
pnpm i @nestjs/config
Use this to inject environment variables securely into your application

References
Drizzle ORM PostgreSQL guide: https://orm.drizzle.team/docs/get-started/postgresql-new

