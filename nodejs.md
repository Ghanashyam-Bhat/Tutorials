### Download
Node Package Manager (npm)
Node Version Manager (nvm)
MongoDB and MongoCompass

### Use Node version 16.18.0 
npm init -y
npm install

### npm install
npm install express
npm install express-session

npm install mongod
npm install mongo
npm install mongoose

npm install cookie-parser
npm install cors


### Error connecting MongoDB - Use  <code> mongodb://127.0.0.1:27017/testdatabase</code>  instead of <code>mongodb://localhost:27017/testdatabase </code> 


### Structuring of NodeJs application for better maintainance
- app
  - controllers
    - UserController.js
    - ...
  - models
    - User.js
    - ...
  - routes
    - index.js
    - userRoutes.js
    - ...
  - services
    - AuthService.js
    - ...
  - utils
    - validation.js
    - ...
- config
  - database.js
  - ...
- middleware
  - authMiddleware.js
  - ...
- index.js


Let's break down the purpose of each directory:

app/controllers: This directory holds the controllers responsible for handling specific routes or endpoints. For example, UserController.js would contain functions related to user-related operations.

app/models: The models directory houses the Mongoose schemas representing your data structures. For instance, User.js would define the user schema and related methods.

app/routes: This directory contains route files responsible for mapping incoming requests to the appropriate controller functions. index.js can serve as the entry point for all routes, and additional route files like userRoutes.js can handle user-related routes.

app/services: Services encapsulate business logic that may be required across multiple controllers. For example, AuthService.js could contain functions related to authentication and session management.

app/utils: Utility functions that are used across different parts of the application can be placed here. For example, validation.js could contain functions for input validation or data formatting.

config: The config directory stores configuration files for different aspects of your server, such as database connections (database.js) or environment variables.

middleware: Middleware functions can be placed in this directory. For instance, authMiddleware.js could handle authentication-related middleware.

index.js: This is the entry point of your application, where you set up the server, import necessary modules, and define the main server logic.