# react-notes

_based on Steven Griders's [Node with React Fullstack Web Development](www.udemy.com/node-with-react-fullstack-web-development) cource available on [Udemy](www.udemy.com)._

## server NPM modules

### Essentials

- `express`...the API backbone
- `mongoose`...hint: define a model!
- `cookie-session`...save the user ID client side, or use
- `express-session` to store server side (beware of the default in-memory store!)
- `passport`...for authentication
- `passport-google-oauth20`...or use a local strategy
- `body-parser`...may not be necessary if all post data handled via SPA

### Extras

- `morgan`...logging to the console made easy
- `colors`...liven up your console

## client NPM modules

- `redux`...predictable state/store container
- `react-redux`...official React bindings, the glue between React and Redux
- `axios`...HTTP client to make ajax requests
- `redux-thunk`...takes the response from a request, used to delay the dispatch of an action, or to dispatch only if a certain condition is met, provides direct access to the dispatch function
- `react-router-dom`...DOM aware module, depends on `react-dom`
- `materialize-css`...for style

## pre-installed NPM modules when `create-react-app` is used

- `react`...user interface base package
- `react-dom`...not directly used in project, included in `react-router-dom`
- `react-scripts`...configuration scripts used by `create-react-app`

## dev tools

- `concurrently -g`...run express and react dev server with one command
- `create-react-app -g`...used for initial SPA creation
- `http-proxy-middleware --save`...proxy react dev server thru express

## dev environment

- `package.json` server scripts:

```
"scripts": {
    "start": "node index.js",
    "server": "nodemon index.js",
    "client": "npm run start --prefix client",
    "dev": "concurrently \"npm run client\" \"npm run server\""
}
```

- delete all boilerplate code within `src` folder except serviceWorker.js
- express server listens on port 5000, react dev server listens on port 3000
- create `setupProxy.js` within the client source file:

```
const proxy = require('http-proxy-middleware');

module.exports = app => {
  app.use(proxy('/auth/google', { target: 'http://localhost:5000' }));
  app.use(proxy('/api/*', { target: 'http://localhost:5000' }));
};
```

## react/redux cycle

1. A **React Component** (`react`) calls...
2. An **Action Creator**, (`axios`) which produces...
3. An **Action**, (`redux`) this is sent to...
4. A **Dispatch Function**, (`redux-thunk`) which may or may not provide info to one or more
5. **Reducers**, (`redux`) which updates the state in...
6. The **Store**, (`redux`) which is sent back to the React components causing them to re-render
