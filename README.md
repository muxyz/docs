# MU Docs

Welcome to the MU documentation. Here you will learn how to create an app using MU.app and what functionality is provided in via the `window.mu` object.

## Before you start

Creating an app with Mu is easy because it's just a tradional website. Just use HTML, JS and CSS and you're good to go. All code is rendered within the <body> tags of our renderer (which is just a server rendered HTML page).

If you want routing in your application this can be done through a Single page application router like React Router or Vue Router etc.

Our main application (mu.app) then uses an <iframe> to load your content via ourrenderer. Our renderer has some functionality attached to the `window` that allows you to interact with the server and also provides lot of functionality out of the box.


## User authentication

All apps that are created from within the Mu application have access to logged in user. You can access the user via `mu.user`.

Here you have two values:
- `authenticated`: This is a boolean that is true once the server has finished authenticating the user.
- `details`: This is the users details. If `details` is `undefined` and `authenticated` is true, this indicates the user is not loggedin
  
