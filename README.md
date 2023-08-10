# MU Docs

Welcome to the MU documentation!

Here you will learn how to create an app using MU.app and what functionality is provided in via the `window.mu` object.

## How it works

Creating an app with Mu is easy as pie because a Mu app is just a traditional website. Just use HTML, JS and CSS and you're good to go. All code is rendered within the `<body>` tags of our renderer (which is just a server rendered HTML page).

> Note: If you want routing in your app, this can be done through a Single Page Application router like React Router or Vue Router etc.

Our renderer has some useful functionality attached to the `window` via `window.mu` or `mu` object. This allows you to interact with the local server and also provides User Authentication via `mu.user`, Database storage via `mu.storage` and payments via `mu.payments`.

## mu.user

All apps that are created from within the Mu application have access to logged in user via `mu.user`. See below for a list of properties and methods:

#### `authenticate()`

Used to authenticate the user. Authenticate is usually run when your app is first rendered (only if you need your user to be authenticated within your application).

#### `getUser: () => User | undefined`

Call this function to get the currently logged in user. This will return `undefined` if you haven't previously called authenticate or the user is not logged in.

Here is an example of the `User` interface:

```
{
	created: "1686737802",
	email: "test@email.com",
	id: "683d319b-59db-4129-84f2-4662cc48bd02",
	profile: {
		profilePicture: 'profile-picture.jpg'
	},
	updated: "1690380034"
	username: "username"
	verification_date: "1690380034"
	verified: true
}
```

#### `authenticated`

Returns a boolean as to whether the `authenticate` call has previously finished. This is helpful to test that the user is not logged in.

## mu.storage

Mu Storage allows a developer to create a table for their application or entity.

> Tables are namespaced to your application ID, so there will not be clashes with other users table names.

To add storage to your app you simply need to call the the `mu.storage` function with the `name` of the entity you'd like to create.

Once this is called your app now has DB storage and the UI can interact with the DB.

```javascript
// Todos example:
const todos = mu.storage("todos");

async function getTodos() {
  const user = mu.user.getUser();
  const response = await todos.find({ where: { creator: user.id } });
  console.log(response);
}

getTodos().catch((e) => {
  console.log("handle error", e);
});
```

Wait... The UI writes directly into the database?! Not exactly, that would be incredibly terrible.

Currently all reads are public, but other CRUD routes are locked to the creator of the row. Fully private storage is on the roadmap if you would like this sooner then please raise and issue in Github.

** As Mu is in beta this is subject to change. All feedback is welcomed**

#### `create`

Mu storage is schemaless and allows users to specify how they want their data to be stored. When passing a record to `create` it is instantly created in the database.

** create requires the user to be logged in. This is for security reasons**

```javascript
const todos = mu.storage("todos");

async function createTodo({ todo }) {
  const response = await todos.create({
    todo,
    completed: false,
  });

  console.log(response);
}

createTodo().catch((e) => {
  console.log("handle error", e);
});
```
