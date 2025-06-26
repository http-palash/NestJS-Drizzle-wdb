# Setting Up a NestJS Project with Drizzle and PostgreSQL

## Installation

Install the NestJS CLI globally:

```bash
npm install -g @nestjs/cli
```

OR to ensure the latest version:

```bash
npm install -g @nestjs/cli@latest
```

Create a new NestJS project with pnpm as the package manager:

```bash
nest new nestjs-drizzle
```

When prompted, choose `pnpm` as the package manager.

Install core NestJS dependencies:

```bash
npm install @nestjs/common @nestjs/core
```

## Project Structure

### `src` Directory

1. **`main.ts`**
   - **Purpose**: Entry point of the application.
   - **Details**:
     - Calls the `bootstrap` function to create the application using the `AppModule`.
     - Starts the Express HTTP server by calling `app.listen(3000)` to listen for HTTP connections on port 3000.
     - Enables HTTP operations at this endpoint.

2. **`app.module.ts` (AppModule)**
   - **Purpose**: Central module to wire up controllers and providers.
   - **Details**:
     - Initializes `AppController` as a controller.
     - Registers `AppService` as a provider.
     - **Provider**: Can be injected into other parts of the application via dependency injection.
     - **Controller**: Entry point for HTTP traffic.

3. **`app.controller.ts`**
   - **Purpose**: Handles HTTP requests.
   - **Details**:
     - Decorated with `@Controller` to mark it as a controller.
     - Injects `AppService` via the constructor for dependency injection.
     - Exposes a single `@Get` route that calls the `getHello()` function from `AppService`.

4. **`app.service.ts`**
   - **Purpose**: Contains business logic.
   - **Details**:
     - Marked with `@Injectable` decorator, enabling dependency injection into other NestJS classes.
     - Contains a `getHello()` function that returns a string.
     - Registered as a provider, allowing it to be injected into controllers or other services.

**Note**: All providers and controllers are wired together in `AppModule`, which is bootstrapped by the `bootstrap` function in `main.ts`.

## Starting the Project

In `package.json`, the following script is used to run the project in development mode:

```json
{
  "scripts": {
    "start:dev": "nest start --watch"
  }
}
```

- **Purpose**: The `start:dev` script runs the project in watch mode, automatically recompiling on code changes.

## Setting Up Docker and PostgreSQL

### Enable Windows Features (Windows Users)

Enable Hyper-V and Containers:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName $("Microsoft-Hyper-V", "Containers") -All
```

### Install WSL and Docker

Install WSL (Windows Subsystem for Linux):

```bash
wsl --install
```

Check installed WSL distributions:

```bash
wsl --list --verbose
```

Build and start the Docker containers:

```bash
docker-compose up --build
```

### Docker Compose Configuration

Set up a `docker-compose.yml` file to run a PostgreSQL container:

```yaml
version: '3.8'
services:
  postgres:
    image: postgres:latest
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: example
      POSTGRES_DB: mydatabase
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

### Install pgAdmin 4

Download and install pgAdmin 4 from:

[pgAdmin 4 Download](https://www.postgresql.org/ftp/pgadmin/pgadmin4/v9.4/windows/)

### Connect pgAdmin to PostgreSQL

1. Open pgAdmin 4.
2. Register a server:
   - **Name**: Local
   - **Host**: localhost
   - **Port**: 5432
   - **Username**: postgres
   - **Password**: example
   - **Database**: mydatabase

## Integrating Drizzle ORM

Install Drizzle ORM and related dependencies:

```bash
pnpm add drizzle-orm pg
pnpm add -D drizzle-kit @types/pg
```

### Configure Environment Variables

Install the NestJS config module to manage environment variables:

```bash
pnpm i @nestjs/config
```

**Note**: The `@nestjs/config` package allows injecting environment variables into the application using NestJS's configuration system.

## Reference

For more details on using Drizzle ORM with PostgreSQL, refer to the official documentation:

[Drizzle ORM PostgreSQL Guide](https://orm.drizzle.team/docs/get-started/postgresql-new)
