---
created: 2024-08-01T08:33
updated: 2024-08-01T08:42
---
# Introduction
## Why NestJS?
### NestJS Overview
- NestJS offers a well-structured module system, making it more flexible and maintainable compared to other frameworks.
- It addresses key issues such as:
    - `Modularity`
    - `Dependency Injection`
    - `Scalability`
    - Extensive `documentation` and `support` for a wide range of libraries within its ecosystem
- **Structured Approach**:
    - `Scales` effectively with team growth
    - Ensures code `consistency`
    - Focuses on business logic
- Provides useful `out-of-the-box` features

### What is NestJS?

- NestJS is an efficient and scalable Node.js backend framework that delivers a structured, modular architecture inspired by Angular.
- It supports robust HTTP server frameworks like **Express** (the default) and can also be configured to use **Fastify**.
- It is written in TypeScript but also supports pure JavaScript (though TypeScript is recommended).

## Installation

Global CLI
```bash
npm i -g @nestjs/cli
```

- create new nest project
```bash
nest new project-name
```

## Project Structure
![[project-structure.png]](./../../../assets/blog/tech/nestjs/project-structure.png)
this is my own project structure I used in my projects

- src
	- features
		- featureName
			- featureName.**controller.spec**.ts : feature controller unit testing
			- featureName.**controller**.ts: feature controller which contain http methods like (GET, POST, PUT, DELETE,....)
			- featureName.**service**.ts
	- common
		- util.ts :  Utility functions
	- app.**module**.ts
	- main.ts

## Modules
![[modules-hirearchy.png]](./../../../assets/blog/tech/nestjs/modules-hirearchy.png)
Each module represent as a folder which contain these components or more and configure them in module file (moduleName.module.ts):
- service (contains business logic and usually use DB ORM/ODM services in it)
- controller
- entity / schema
### moduleName.module.ts
**Definition:** A File or class annotated with a `@Module()` decorator.
**Job:** Contains metadata which configure project stucture and make it easy to use module components and manage them.

For Example this is a user module:
``` ts
import { Module } from '@nestjs/common';
import { UserService } from './user.service';
import { UserController } from './user.controller';

@Module({
  controllers: [UserController],
  providers: [UserService],
})
export class UserModule { }
```

### App module (**root module**)
Each feature module must be inject in app.module.ts file to configure it when create app (Express/Fastify) module in main.ts (index file which run server)
```ts
import { Module } from '@nestjs/common';

import { CustomConfigModule } from '@config/config.module';
import { UserModule } from '@user/user.module';
  

@Module({
  imports: [
    CustomConfigModule,
    UserModule
  ]
})

export class AppModule { }
```
## Dependencies
we will explain nestJS Dependencies and you can find it in node_modules after install nestjs or can breifly see it in **package.json** file
##### 1- Platforms
- **platform-express**
- **platform-fastify**

in **main.ts** at bootstrap function you defined which platform will be chosen

```ts
// using ExpressJS
const app = await NestFactory.create<NestExpressApplication>(AppModule);

// or using fastify
const app = await NestFactory.create<NestFastifyApplication>(  
AppModule,  
new FastifyAdapter(),  
);

//or it's by default use ExpressJS
const app = await NestFactory.create(AppModule);
```

##### 2- TypeScript and Types

##### 3- Linting (ES-lint)

##### 4- formatting (prettierr)
##### 5- Unit testing (Jest)