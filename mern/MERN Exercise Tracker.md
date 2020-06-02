# MERN Exercise Tracker

*source*: https://youtu.be/7CqJlxBYj-M 60m

##### Prerequisite

- Create MongoDB Atlas account (MongoDB in the cloud) and cluster
  - don't forget to respecify IP whitelist when changing place
  - don't forget constraints (foreign key)
- Install node.js (and VSCode)
- Install Insomnia (or Postman) to test the routes

##### Set-up project

```bash
npx create-react-app <name> # create react project (installs react if necessary)
mkdir backend 				# create backend folder
cd backend
npm init -y 				# create package.json file

npm install express cors mongoose dotenv # install dependencies
npm install -g nodemon 				# global install (restart server when file changes)
```

#### Back-end

##### Create server

server.js file < 

- specify required libraries
- create server and port
- say it uses required libraries
- make server listen on port

```bash
backend> nodemon server # start server using file server
```

##### Set-up DB connection

- .env < DB uri (available on Atlas's dashboard)
- connect to DB
- open connection

##### Create DB schema with mongoose (gives function such as find and save to DB)

- models folder < exercise.model.js, user.model.js
- code schema: require mongoose, pass dictionary of attributes to schema constructor, create and export one

##### Add API endpoint Routes to allow server to perform CRUD (Create Read Update Delete)

- routes folder < exercises.js, users.js
  - users.js < 
    - require express router, user model
    - create routes with URI, http method and callback on request and response objects
    - export router
  - exercises.js < same as users. When saving exercises, convert the data to the expected type
- tell server to use them (require file, use)

##### Test Routes

- create requests in Insomnia and send them (to running server). When we add users (e.g.) we can see that MongoDB automatically adds *id*, *created_at* and *updated_at* fields
- We can view and edit the collections in MongoDB Atlas

#### Front-end

React is a JS library that allows to build complex UIs by developing and composing smaller components.

##### React Component Basics

- create: `class ShoppingList extends React.Component {render(){return(My JSX code)}}`
  - prefix by `export default` to expose this class to other modules
- `render()` returns the representation of the component. It is written in JSX (HTML-like + JS interpolated in {})
- Call in HTML: ```<ShoppingList name="Alice" />``` name is a property of the class

##### App

- `index.js` loads `App.js` (contains all -the layout- of our react app) into the `<body id="root"></body>` tag of `index.html`

```bash
mern-ex> npm start # start the app with live reload
ex> npm install bootstrap
ex> npm install react-router-dom # allows to load a component when going to a url
```

- puts the routes inside `<Router><Route path="" exact component={}/><Router>`
  - load `component` when going to`path` url
  - `component` to be loaded, don't forget to import it in the file 

##### Components

`<Link to=""></Link>` tag instead of `<a href=""></a>` to link to other components

`className` instead of `class` attribute

