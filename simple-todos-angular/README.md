Todo App with AngularJS
=======================

Creating your first angular-meteor app:
https://www.meteor.com/tutorials/angular/creating-an-app

Table of Contents
-----------------

1. Creating an app
2. Templates
3. Collections
4. Forms and events
5. Update and remove
6. Deploying your app
7. Running on mobile
8. Filtering Collections
9. Adding user accounts
10. Security with methods
11. Publish and subscribe
12. Next steps

1. Creating an app
-------------------

### Instructions

To create a Meteor app, open your terminal and type:

```sh
$ meteor create simple-todos-angular
```

To run the newly created app:

```sh
$ cd simple-todos-angular
$ meteor
```

Open your web browser and go to `http://localhost:3000` to see the app running.

### In my terminal emulator:

```sh
Shoichi at sho-mbp in ~/meteor-tutorials on master
$ ls
README.md             simple-todos/         simple-todos-angular/ simple-todos-react/
c
Shoichi at sho-mbp in ~/meteor-tutorials on master
$ meteor create simple-todos-angular
Created a new Meteor app in 'simple-todos-angular'.

To run your new app:
  cd simple-todos-angular
  meteor

If you are new to Meteor, try some of the learning resources here:
  https://www.meteor.com/learn


Shoichi at sho-mbp in ~/meteor-tutorials on master [?]
$ cd simple-todos-angular/

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [?]
$ ls -al
total 24
drwxr-xr-x   7 Shoichi  staff   238B 19 Nov 17:44 ./
drwxr-xr-x@  7 Shoichi  staff   238B 13 Nov 18:56 ../
-rw-r--r--   1 Shoichi  staff     0B 13 Nov 18:57 .gitkeep
drwxr-xr-x  10 Shoichi  staff   340B 19 Nov 17:45 .meteor/
-rw-r--r--   1 Shoichi  staff    31B 19 Nov 17:44 simple-todos-angular.css
-rw-r--r--   1 Shoichi  staff   233B 19 Nov 17:44 simple-todos-angular.html
-rw-r--r--   1 Shoichi  staff   478B 19 Nov 17:44 simple-todos-angular.js

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [?]
$ git mv .gitkeep README.md

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [+!?]
$ meteor
[[[[[ ~/meteor-tutorials/simple-todos-angular ]]]]]

=> Started proxy.
=> Started MongoDB.
=> Started your app.

=> App running at: http://localhost:3000/
```

2. Templates
------------

### Instructions

To use Angular in our app, we first need to remove the default UI package of Meteor, called Blaze.

We also need to remove Meteor's default ECMAScript2015 package named ecmascript because Angular-Meteor uses a package named angular-babel in order to get both ECMAScript2015 and AngularJS DI annotations.

We remove the default UI package of Meteor called `Blaze` and Meteor's default ECMAScript2015 package named `ecmascript` by running:

```sh
$ meteor remove blaze-html-templates
$ meteor remove ecmascript
```

### In my terminal emulator:

3. Collections
--------------



4. Forms and events
-------------------



5. Update and remove
--------------------



6. Deploying your app
---------------------



7. Running on mobile
--------------------



8. Filtering Collections
------------------------



9. Adding user accounts
-----------------------



10. Security with methods
-------------------------



11. Publish and subscribe
-------------------------



12. Next steps
--------------

