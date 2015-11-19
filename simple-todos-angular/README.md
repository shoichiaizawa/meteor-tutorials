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

This will create a new folder called simple-todos-angular with all of the files that a Meteor app needs:

```
simple-todos-angular.js       # a JavaScript file loaded on both client and server
simple-todos-angular.html     # an HTML file that defines our main view
simple-todos-angular.css      # a CSS file to define your app's styles
.meteor                       # internal Meteor files
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

### Generated html, js, css files

##### simple-todos-angular.html

```html
<head>
  <title>simple-todos-angular</title>
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

##### simple-todos-angular.js

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

##### simple-todos-angular.css

```css
/* CSS declarations go here */
```

2. Templates
------------

### Instructions

To use Angular in our app, we first need to remove the default UI package of Meteor, called Blaze.

We also need to remove Meteor's default ECMAScript2015 package named ecmascript because Angular-Meteor uses a package named angular-babel in order to get both ECMAScript2015 and [AngularJS DI annotations](https://docs.angularjs.org/guide/di).

We remove the default UI package of Meteor called `Blaze` and Meteor's default ECMAScript2015 package named `ecmascript` by running:

```sh
$ meteor remove blaze-html-templates
$ meteor remove ecmascript
```
Now we need to add the angular-meteor package by typing the following command into the command line:

```
$ meteor add angular
```

To start working on our todos list app, let's replace the code of the default starter app with the code below. Then we'll talk about what it does.

#### 2.2  Add Angular app and controller to HTML

```html
<head>
  <title>Todo List</title>
</head>
 
<body>
<div class="container"
     ng-app="simple-todos"
     ng-controller="TodosListCtrl">
</div>
</body>
```

#### 2.3  Init Angular app and controller simple-todos-angular.js »

```javascript
if (Meteor.isClient) {
 
  // This code only runs on the client
  angular.module('simple-todos',['angular-meteor']);
 
  angular.module('simple-todos').controller('TodosListCtrl', ['$scope',
    function ($scope) {
 
      $scope.tasks = [
        { text: 'This is task 1' },
        { text: 'This is task 2' },
        { text: 'This is task 3' }
      ];
 
  }]);
}
```

#### 2.4  Add Angular list to template simple-todos-angular.html »

```html
<div class="container"
     ng-app="simple-todos"
     ng-controller="TodosListCtrl">
 
  <header>
    <h1>Todo List</h1>
  </header>
 
  <ul>
    <li ng-repeat="task in tasks">{{task.text}}</li>
  </ul>
 
</div>
</body>
```

#### Adding CSS

```css
/* CSS declarations go here */
body {
  font-family: sans-serif;
  background-color: #315481;
  background-image: linear-gradient(to bottom, #315481, #918e82 100%);
  background-attachment: fixed;

  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;

  padding: 0;
  margin: 0;

  font-size: 14px;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  min-height: 100%;
  background: white;
}

header {
  background: #d2edf4;
  background-image: linear-gradient(to bottom, #d0edf5, #e1e5f0 100%);
  padding: 20px 15px 15px 15px;
  position: relative;
}

#login-buttons {
  display: block;
}

h1 {
  font-size: 1.5em;
  margin: 0;
  margin-bottom: 10px;
  display: inline-block;
  margin-right: 1em;
}

form {
  margin-top: 10px;
  margin-bottom: -10px;
  position: relative;
}

.new-task input {
  box-sizing: border-box;
  padding: 10px 0;
  background: transparent;
  border: none;
  width: 100%;
  padding-right: 80px;
  font-size: 1em;
}

.new-task input:focus{
  outline: 0;
}

ul {
  margin: 0;
  padding: 0;
  background: white;
}

.delete {
  float: right;
  font-weight: bold;
  background: none;
  font-size: 1em;
  border: none;
  position: relative;
}

li {
  position: relative;
  list-style: none;
  padding: 15px;
  border-bottom: #eee solid 1px;
}

li .text {
  margin-left: 10px;
}

li.checked {
  color: #888;
}

li.checked .text {
  text-decoration: line-through;
}

li.private {
  background: #eee;
  border-color: #ddd;
}

header .hide-completed {
  float: right;
}

.toggle-private {
  margin-left: 5px;
}

@media (max-width: 600px) {
  li {
    padding: 12px 15px;
  }

  .search {
    width: 150px;
    clear: both;
  }

  .new-task input {
    padding-bottom: 5px;
  }
}
```

### In my terminal emulator:

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master
$ meteor remove blaze-html-templates

Changes to your project's package version selections:

blaze-html-templates   removed from your project
caching-compiler       removed from your project
caching-html-compiler  removed from your project
templating             removed from your project
templating-tools       removed from your project

blaze-html-templates: removed dependency

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ meteor remove ecmascript
ecmascript: removed dependency

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ meteor add angular

Changes to your project's package version selections:

angular                             added, version 1.2.2
angular-meteor-data                 added, version 0.0.6
angular-templates                   added, version 0.0.1
angular:angular                     added, version 1.4.7
caching-compiler                    added, version 1.0.0
caching-html-compiler               added, version 1.0.2
dburles:mongo-collection-instances  added, version 0.3.4
lai:collection-extensions           added, version 0.1.4
pbastowski:angular-babel            added, version 1.0.4
templating-tools                    added, version 1.0.0


angular: Everything you need to use AngularJS in your Meteor app

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ vim simple-todos-angular.html

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.html
diff --git a/simple-todos-angular/simple-todos-angular.html b/simple-todos-angular/simple-todos-angular.html
index 30ca9b0..745ec7a 100644
--- a/simple-todos-angular/simple-todos-angular.html
+++ b/simple-todos-angular/simple-todos-angular.html
@@ -1,14 +1,23 @@
 <head>
-  <title>simple-todos-angular</title>
+  <title>Todo List</title>
 </head>

 <body>
-  <h1>Welcome to Meteor!</h1>
+  <div class="container"
+       ng-app="simple-todos"
+       ng-controller="TodosListCtrl">
+    <header>
+      <h1>Todo List</h1>
+    </header>

-  {{> hello}}
+    <ul>
+      <li ng-repeat="task in tasks">{{task.text}}</li>
+    </ul>
+
+  </div>
 </body>

-<template name="hello">
-  <button>Click Me</button>
-  <p>You've pressed the button {{counter}} times.</p>
-</template>
+<!-- <template name="hello"> -->
+  <!-- <button>Click Me</button> -->
+  <!-- <p>You've pressed the button {{counter}} times.</p> -->
+<!-- </template> -->

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ vim simple-todos-angular.js

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.js
diff --git a/simple-todos-angular/simple-todos-angular.js b/simple-todos-angular/simple-todos-angular.js
index 4f8c65d..0f3309c 100644
--- a/simple-todos-angular/simple-todos-angular.js
+++ b/simple-todos-angular/simple-todos-angular.js
@@ -1,23 +1,22 @@
 if (Meteor.isClient) {
-  // counter starts at 0
-  Session.setDefault('counter', 0);

-  Template.hello.helpers({
-    counter: function () {
-      return Session.get('counter');
-    }
-  });
+  // This code only runs on the client
+  angular.module('simple-todos',['angular-meteor']);

-  Template.hello.events({
-    'click button': function () {
-      // increment the counter when button is clicked
-      Session.set('counter', Session.get('counter') + 1);
-    }
-  });
-}
+  angular.module('simple-todos').controller('TodosListCtrl', ['$scope',
+    function ($scope) {
+
+      $scope.tasks = [
+        { text: 'This is task 1' },
+        { text: 'This is task 2' },
+        { text: 'This is task 3' }
+      ];

-if (Meteor.isServer) {
-  Meteor.startup(function () {
-    // code to run on server at startup
-  });
+  }]);
 }
+
+/* if (Meteor.isServer) {
+ *   Meteor.startup(function () {
+ *     // code to run on server at startup
+ *   });
+ * } */

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$
```

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

