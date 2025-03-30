# `server.js` Workflow Explanation

The `server.js` file is the main entry point for the server of the `cloudscape` web application. This document provides an explanation of the workflow and the code snippets used in this file.

## Imports and Requires

```javascript
import 'dotenv/config'
import express from 'express';
import configViewEngine from './src/config/configEngine';
import routes from './src/routes/web';
import cronJobContronler from './src/controllers/cronJobContronler';
import socketIoController from './src/controllers/socketIoController';
const cors = require('cors');
require('dotenv').config();
let cookieParser = require('cookie-parser');
```
dotenv/config: Loads environment variables from a .env file.
express: A web framework for Node.js.
configViewEngine: Custom module for configuring the view engine.
routes: Custom module for defining web routes.
cronJobContronler: Custom module for managing cron jobs.
socketIoController: Custom module for managing Socket.io connections.
cors: Middleware for enabling Cross-Origin Resource Sharing (CORS).
cookie-parser: Middleware for parsing cookies.

CORS Configuration
```js
const corsOptions = {
    origin: 'https://api.bulkcampaigns.com', // Allow only requests from this origin
    methods: 'GET,POST', // Allow only these methods
    allowedHeaders: ['Content-Type', 'Authorization'],
    optionsSuccessStatus: 200 // Allow only these headers
};
```
Configures CORS to allow requests only from https://api.bulkcampaigns.com.
Permits GET and POST methods.
Allows Content-Type and Authorization headers.

Express Application Setup
```js
const app = express();
app.use(cors());
const server = require('http').createServer(app);
const io = require('socket.io')(server);
```
Creates an instance of an Express app.
Uses CORS middleware.
Sets up HTTP server and Socket.io server.

Middleware Configuration

```js
app.use(cookieParser());
app.use(express.urlencoded({ extended: true }));
app.use(express.json());
```
Uses cookie parsing middleware.
Configures Express to parse URL-encoded and JSON request bodies.

View Engine and Routes
```js
configViewEngine(app);
routes.initWebRouter(app);
```
Sets up the view engine using configViewEngine.
Initializes web routes with routes.initWebRouter.

Socket.io and Cron Jobs
```js
cronJobContronler.cronJobGame1p(io);
socketIoController.sendMessageAdmin(io);
```
Initializes a cron job for a game using cronJobContronler.
Monitors connections to the server with socketIoController.
Server Initialization
```js
const port = process.env.PORT;
server.listen(port, () => {
    console.log("http://localhost:" + port);
});
```
Starts the server on the port specified in the environment variables.
Logs the server URL to the console.


Complete Code
```js
import 'dotenv/config'
import express from 'express';
import configViewEngine from './src/config/configEngine';
import routes from './src/routes/web';
import cronJobContronler from './src/controllers/cronJobContronler';
import socketIoController from './src/controllers/socketIoController';
const cors = require('cors');
require('dotenv').config();
let cookieParser = require('cookie-parser');

const corsOptions = {
    origin: 'https://api.bulkcampaigns.com',
    methods: 'GET,POST',
    allowedHeaders: ['Content-Type', 'Authorization'],
    optionsSuccessStatus: 200
};

const app = express();
app.use(cors());
const server = require('http').createServer(app);
const io = require('socket.io')(server);

const port = process.env.PORT;

app.use(cookieParser());
app.use(express.urlencoded({ extended: true }));
app.use(express.json());

configViewEngine(app);
routes.initWebRouter(app);

cronJobContronler.cronJobGame1p(io);
socketIoController.sendMessageAdmin(io);

server.listen(port, () => {
    console.log("http://localhost:" + port);
});
```
This document provides an overview of the workflow and setup of the server.js file in the cloudscape repository.
