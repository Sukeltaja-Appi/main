# sukeltaja-backend documentation

## 🐗 Quick start

1. `git clone https://github.com/Sukeltaja-App/sukeltaja-backend.git`
2. `cd sukeltaja-backend`
3. `npm install`
4. `npm run watch`

## ℹ General information

Tools and frameworks used for backend:

* [Node.js](https://nodejs.org/)
* [Mongoose](https://mongoosejs.com/)
* [Express](https://expressjs.com/)
* [SocketIO](https://socket.io/)

### Miscellanneous information

* Backend currently runs on [Heroku](https://www.heroku.com/). The data is stored in MongoDB @ [MongoDB Atlas](https://www.mongodb.com/).
* [Back office](https://github.com/Sukeltaja-App/sukeltaja-bo) (browser-frontend) build runs at backend root.
* Enviroment variables are loaded with [dotenv](https://www.npmjs.com/package/dotenv) from an .env file. These values are used and set at config.js file for backend. From there, you can check what you need to provide.
* Tokens are created with [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken).

## Testing

* Testing the backend is done with [supertest](https://www.npmjs.com/package/supertest).
* Testing currently uses a real database @ [MongoDB Atlas](https://www.mongodb.com/), and sometimes fails when two sets of same tests run simultaneously. (Eg. pull requests testing current branch + merge branch)
* Tests create and store mock data to database before and during the tests.

## Target data

[About the target data in the backend](targets.md).