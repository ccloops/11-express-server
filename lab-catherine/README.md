# Code Fellows: Seattle 401 JavaScript - 401d19

##  Lab 11 && 12: Express and Mongo REST API

### Author:
 Catherine Looper

### Motivation

In this project, I built a RESTful (Hypertext Transfer Protocol) HTTP server using Express. This server handles GET, POST, PUT and DELETE requests/responses. This API uses MongoDB and Mongoose to write data to a db directory for persistence.

### Build

#### Server Module

The server module is creating an http server, defining server-on behavior and exporting an interface for starting and stopping the server. The server module exports an object containing start and stop methods.

The server module requires in express, mongoose, logger and the book-router.js file. The server.start and stop methods return a new Promise with resolve and reject parameters. The start method contains an app.listen function that listens for the server start. The server.stop method has an httpServer.close function that turns the server off by setting the isServerOn variable to false.

#### Route Module

##### `book-router.js`

book-router.js requires in the Router object from express, the jsonParser, http-errors, the logger module  and book.js. Inside the module, there are functions declared for bookRouter.post, bookRouter.get, bookRouter.delete, and bookRouter.put. These methods each handle their corresponding method and send the appropriate response based on the input. The bookRouter is exporting a new Router instance.

#### Model Module

The model module contains a book.js file that requires in mongoose and has a bookSchema with the properties: title, author, genre, content, and timestamp. The mongoose.model is being exported from this file.
#### Test Module

server.test.js contains tests for POST, GET, DELETE and PUT methods.

#### Middleware

##### `error-middleware.js`

The error-middleware module handles error messages for a variety of different use cases, including HTTP errors and MONGODB errors. 

* HTTP errors include the following logs: 

 ``` 
  logger.log('info','__ERROR_MIDDLEWARE__');
  logger.log('info',error);

  if(error.status){
    logger.log('info',Responding with a ${error.status} status and message: ${error.message});
    return response.sendStatus(error.status);
  }
  ```
* MONGODB errors include the following logs:

```
  if(message.includes('validation failed')) {
    logger.log('info','Responding with a 400 status code');
    return response.sendStatus(400);
  }

  if(message.includes('duplicate key')) {
    logger.log('info','Responding with a 409 status code');
    return response.sendStatus(409);
  }

  if(message.includes('objectid failed')) {
    logger.log('info','Responding with a 404 status code');
    return response.sendStatus(404);
  }

  if(message.includes('unauthorized')) {
    logger.log('info','Responding with a 401 status code');
    return response.sendStatus(401);
  }
```

* If there is an error that doesn't match the above, then:

```
  logger.log('info', 'Responding with a 500 status code');
  logger.log('info', error);
  return response.sendStatus(500);
```

##### `logger-middleware.js`

The logger-middleware module logs the request method processes and request urls and returns next to continue on in the promise chain.

### Limitations

To use this app - it is assumed that the user has familiarity with the tech and frameworks listed below. 

### Code Style

Standard JavaScript with ES6

### Tech/Framework used

* JavaScript / ES6
* Node.js
* Jest
* Eslint
* MongoDB
* Mongoose
* Winston
* Express
* Superagent
* Dotenv
* Body-Parser
* Faker
* http-errors

### How to use?

* Step 1. Fork and Clone the Repository.
* Step 2. `npm install`.
* Step 3. touch a `.env` file and add the following to the file: `PORT=3000` and `MONGODB_URI=mongodb://localhost/testing`.
* Step 4. start MongoDB by calling `npm run dbon`.
* Step 5. to test the API, open a second terminal window and run the command `npm run test`.
* Step 6. If you would like to start the server, you can run the command `npm run start`.

### Credits

* Code Fellows / Vinicio Vladimir Sanchez Trejo for providing the demo code as reference.

### License

MIT © Catherine Looper