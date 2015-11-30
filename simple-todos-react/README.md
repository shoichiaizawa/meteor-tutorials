Todo App with React
===================

[Creating your first meteor-react app](https://www.meteor.com/tutorials/react/creating-an-app)

Table of Contents
-----------------

1. Creating an app
2. Components
3. Collections
4. Forms and events
5. Update and remove
6. Deploying your app
7. Running on mobile
8. Temporary UI state
9. Adding user accounts
10. Security with methods
11. Publish and subscribe
12. Next steps

1. Creating an app
------------------

### Instructions

To create the app, open your terminal and type:

```sh
$ meteor create simple-todos-react
```

This will create a new folder called simple-todos-react with all of the files that a Meteor app needs:

```
simple-todos-react.js     # a JavaScript file loaded on both client and server
simple-todos-react.html   # an HTML file that defines view templates
simple-todos-react.css    # a CSS file to define your app's styles
.meteor                   # internal Meteor files
```

To run the newly created app:

```sh
$ cd simple-todos-react
$ meteor
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials on master [+!]
$ meteor create simple-todos-react/
Created a new Meteor app in 'simple-todos-react/'.

To run your new app:
  cd simple-todos-react/
  meteor

If you are new to Meteor, try some of the learning resources here:
  https://www.meteor.com/learn


Shoichi at sho-mbp in ~/meteor-tutorials on master [+!?]
$ cd simple-todos-react/

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [+!?]
$ ls -al
total 32
drwxr-xr-x   7 Shoichi  staff   238B 30 Nov 17:50 ./
drwxr-xr-x@  8 Shoichi  staff   272B 24 Nov 20:50 ../
drwxr-xr-x  10 Shoichi  staff   340B 30 Nov 17:51 .meteor/
-rw-r--r--   1 Shoichi  staff   2.0K 30 Nov 17:48 README.md
-rw-r--r--   1 Shoichi  staff    31B 30 Nov 17:50 simple-todos-react.css
-rw-r--r--   1 Shoichi  staff   231B 30 Nov 17:50 simple-todos-react.html
-rw-r--r--   1 Shoichi  staff   478B 30 Nov 17:50 simple-todos-react.js

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [+!?]
$ meteor
[[[[[ ~/meteor-tutorials/simple-todos-react ]]]]]

=> Started proxy.
=> Started MongoDB.
=> Started your app.

=> App running at: http://localhost:3000/
```

### Generated html, js, css files

##### `simple-todos-react.html`

```htlm
<head>
  <title>simple-todos-react</title>
</head>

<body>
  <h1>Welcome to Meteor!</h1>

  {{> hello}}
</body>

<template name="hello">
  <button>Click Me</button>
  <p>You've pressed the button {{counter}} times.</p>
</template>
```

##### `simple-todos-react.js`

```javascript
if (Meteor.isClient) {
  // counter starts at 0
  Session.setDefault('counter', 0);

  Template.hello.helpers({
    counter: function () {
      return Session.get('counter');
    }
  });

  Template.hello.events({
    'click button': function () {
      // increment the counter when button is clicked
      Session.set('counter', Session.get('counter') + 1);
    }
  });
}

if (Meteor.isServer) {
  Meteor.startup(function () {
    // code to run on server at startup
  });
}
```

##### `simple-todos-react.css`

```css
/* CSS declarations go here */
```

2. Components
-------------

### Instructions

### In my terminal emulator

3. Collections
--------------

### Instructions

### In my terminal emulator

4. Forms and events
-------------------

### Instructions

### In my terminal emulator

5. Update and remove
--------------------

### Instructions

### In my terminal emulator

6. Deploying your app
---------------------

### Instructions

### In my terminal emulator

7. Running on mobile
--------------------

### Instructions

### In my terminal emulator

8. Temporary UI state
---------------------

### Instructions

### In my terminal emulator

9. Adding user accounts
-----------------------

### Instructions

### In my terminal emulator

10. Security with methods
-------------------------

### Instructions

### In my terminal emulator

11. Publish and subscribe
-------------------------

### Instructions

### In my terminal emulator

12. Next steps
--------------

### Instructions

### In my terminal emulator

