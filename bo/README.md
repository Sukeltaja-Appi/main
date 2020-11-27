# sukeltaja-bo documentation

## 🐘 Quick start

1. `git clone https://github.com/Sukeltaja-Appi/sukeltaja-bo.git`
2. `cd sukeltaja-bo`
3. `npm install`
4. `npm start`

## 🔨 Building the Back Office

The back office runs on top of the backend. Building was done manually:

1. `git clone https://github.com/Sukeltaja-Appi/sukeltaja-bo.git`
2. `git clone https://github.com/Sukeltaja-Appi/sukeltaja-backend.git`
3. `cd sukeltaja-bo`
4. `npm build`
5. `mv build/ ../sukeltaja-backend/`
6. `cd ../sukeltaja-backend/`
7. `git add .`
8. `git commit -m "I built a new version"`
9. `git push`

This could (should) be automated with for example [Docker](https://www.docker.com/) in the future..

## ℹ General information

Tools and frameworks used for bo:

* [React](https://reactjs.org/)
* [Node.js](https://nodejs.org/)
* [Axios](https://www.npmjs.com/package/axios)
* [React Bootstrap](https://react-bootstrap.github.io)
* [React Redux](https://react-redux.js.org)

### Miscellanneous information

* Backend currently runs on [Heroku](https://www.heroku.com/). The data is stored in MongoDB @ [MongoDB Atlas](https://www.mongodb.com/).
* [Back office](https://github.com/Sukeltaja-Appi/sukeltaja-bo) (browser-frontend) build runs at backend root.
* Enviroment variables are used and set at config.js file for bo. From there, you can check what you need to provide.

## 🙉 Testing

* Testing is done locally with `npm test`
* Some difficulties were met when trying to configure component tests with a Redux Store for Code Coverage with Codacy and Travis. Difficulties were not overcome so the configurations were removed.
