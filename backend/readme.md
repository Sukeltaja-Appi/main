# Info for future developers

Here is a brief guide for the next developers.
This guide is for [Backend](https://github.com/Sukeltaja-App/sukeltaja-backend)


Main language: **Javascript**

Tools and frameworks used for backend:

* [Node.js](https://nodejs.org/)

---
* [Mongoose js](https://mongoosejs.com/)
* [Express js](https://expressjs.com/)
* [SocketIO](https://socket.io/)

## Where to start

After fetching the repository you need to install all the required tools.
This can be done on by typing ```npm install``` on the root folder (Node needs to be installed before).

Backend can be started with ```npm run watch``` to run in development mode.

### Backend

* Backend runs currently on [Heroku](https://www.heroku.com/) and data is stored in MongoDB @ [MongoDB Atlas](https://www.mongodb.com/).
* [Back office](https://github.com/Sukeltaja-App/sukeltaja-bo)(browser-frontend) build runs at Backend root.
* Enviroment variables are load with [Dotenv](https://www.npmjs.com/package/dotenv) from .env file. These values are used and set at config.js file for backend. From there, you can check what you need to provide.
* Testing backend is done with [Supertest](https://www.npmjs.com/package/supertest).
  - Testing uses currently real database @ [MongoDB Atlas](https://www.mongodb.com/), and sometimes fails when two sets of same tests run simultaneously. (Eg. pullrequests testing current branch + merge branch)
  - Tests create and store mock data to database before and during the tests.
* Tokens are created with [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken).
  ```diff
  -Currently tokens are never revoked, and this issue should be fixed in future.
````
