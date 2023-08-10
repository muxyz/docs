 
# MU Docs

Welcome to the MU documentation!

Here you will learn how to create an app using MU.app and what functionality is provided in via the `window.mu` object.

## How it works

Creating an app with Mu is easy because an Mu app is just a tradional website. Just use HTML, JS and CSS and you're good to go. All code is rendered within the `<body>` tags of our renderer (which is just a server rendered HTML page).

> Note: If you want routing in your app, this can be done through a Single page application router like React Router or Vue Router etc.

Our renderer has some functionality attached to the `window` via `window.mu` or `mu` which allows you to interact with the local server and also provides functionality out of the box including User Authentication via `mu.user`, Database storage via `mu.storage` and payments via `mu.payments`.

## mu.user

All apps that are created from within the Mu application have access to logged in user via `mu.user`. See below for a list of properties and methods:

#### `authenticate()`

Call this function to authenticate the user. This is usually run when your app is first loaded (only if you need your user to be authenticated within your application).

#### `getUser: () => User` 

Call this function to get the currently logged in users details. This will return `undefined` if you haven't previously called authenticate or the user is not logged in.

Here is an example of the `User` interface:

```
{
	created: "1686737802",
	email: "test@email.com",
	id: "  683d319b-59db-4129-84f2-4662cc48bd02",
	profile: {
		profilePicture:  'profile-picture.jpg'
	},
	updated: "1690380034"
	username: "username"
	verification_date: "1690380034"
	verified: true
}
```

#### `authenticated`

This will return a boolean as to whether the `authenticate` call has previously finished. This is helpful to test that the user is not logged in. 
