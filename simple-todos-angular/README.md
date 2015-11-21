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

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials on master
$ ls
README.md             simple-todos/         simple-todos-angular/ simple-todos-react/

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

##### simple-todos-angular.html

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

#### 2.3  Init Angular app and controller

##### simple-todos-angular.js

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

#### 2.4  Add Angular list to template

##### simple-todos-angular.html

```html
[...]
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

### In my terminal emulator

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
```

```sh
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
```

```sh
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

### Instructions

3.1  Replace the static array with a Collection

##### simple-todos-angular.js

```javascript
Tasks = new Mongo.Collection('tasks');

if (Meteor.isClient) {

  // This code only runs on the client
  angular.module('simple-todos',['angular-meteor']);

  angular.module('simple-todos').controller('TodosListCtrl', ['$scope', '$meteor',
    function ($scope, $meteor) {

      $scope.tasks = $meteor.collection(Tasks);

    }]);
}
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.js
diff --git a/simple-todos-angular/simple-todos-angular.js b/simple-todos-angular/simple-todos-angular.js
index 0f3309c..5dc180a 100644
--- a/simple-todos-angular/simple-todos-angular.js
+++ b/simple-todos-angular/simple-todos-angular.js
@@ -1,16 +1,14 @@
+Tasks = new Mongo.Collection('tasks');
+
 if (Meteor.isClient) {

   // This code only runs on the client
   angular.module('simple-todos',['angular-meteor']);

-  angular.module('simple-todos').controller('TodosListCtrl', ['$scope',
-    function ($scope) {
+  angular.module('simple-todos').controller('TodosListCtrl', ['$scope', '$meteor',
+    function ($scope, $meteor) {

-      $scope.tasks = [
-        { text: 'This is task 1' },
-        { text: 'This is task 2' },
-        { text: 'This is task 3' }
-      ];
+      $scope.tasks = $meteor.collection(Tasks);

   }]);
 }
@@ -18,5 +16,5 @@ if (Meteor.isClient) {
 /* if (Meteor.isServer) {
  *   Meteor.startup(function () {
  *     // code to run on server at startup
- *   });
+ *   });
  * } */

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$
```

4. Forms and events
-------------------

### Instructions

#### 4.1  Add new task form to template

##### simple-todos-angular.html

```html
[...]
  <header>
    <h1>Todo List</h1>

    <!-- add a form below the h1 -->
    <form class="new-task" ng-submit="addTask(newTask); newTask='';">
      <input ng-model="newTask" type="text"
             name="text" placeholder="Type to add new tasks" />
    </form>

  </header>

  <ul>
[...]
```

#### 4.2  Create Add Task scope function

##### simple-todos-angular.js

```javascript
[...]
      $scope.tasks = $meteor.collection(Tasks);

      $scope.addTask = function (newTask) {
        $scope.tasks.push( {
          text: newTask,
          createdAt: new Date() }
        );
      };

    }]);
}
```

#### 4.3  Sort task list by date

##### simple-todos-angular.js

```javascript
[...]
  angular.module('simple-todos').controller('TodosListCtrl', ['$scope', '$meteor',
    function ($scope, $meteor) {

      $scope.tasks = $meteor.collection( function() {
        return Tasks.find({}, { sort: { createdAt: -1 } })
      });

      $scope.addTask = function (newTask) {
        $scope.tasks.push( {
[...]
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.html
diff --git a/simple-todos-angular/simple-todos-angular.html b/simple-todos-angular/simple-todos-angular.html
index 913106e..0c78c28 100644
--- a/simple-todos-angular/simple-todos-angular.html
+++ b/simple-todos-angular/simple-todos-angular.html
@@ -9,6 +9,13 @@

     <header>
       <h1>Todo List</h1>
+
+      <!-- add a form below the h1 -->
+      <form class="new-task" ng-submit="addTask(newTask); newTask='';">
+        <input ng-model="newTask" type="text"
+               name="text" placeholder="Type to add new tasks" />
+      </form>
+
     </header>

     <ul>
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.js
diff --git a/simple-todos-angular/simple-todos-angular.js b/simple-todos-angular/simple-todos-angular.js
index 5dc180a..722d230 100644
--- a/simple-todos-angular/simple-todos-angular.js
+++ b/simple-todos-angular/simple-todos-angular.js
@@ -8,7 +8,16 @@ if (Meteor.isClient) {
   angular.module('simple-todos').controller('TodosListCtrl', ['$scope', '$meteor',
     function ($scope, $meteor) {

-      $scope.tasks = $meteor.collection(Tasks);
+      $scope.tasks = $meteor.collection( function() {
+        return Tasks.find({}, { sort: { createdAt: -1 } })
+      });
+
+      $scope.addTask = function (newTask) {
+        $scope.tasks.push( {
+          text: newTask,
+          createdAt: new Date() }
+        );
+      };

   }]);
 }

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$
```

5. Update and remove
--------------------

### Instructions

#### 5.1  Add done and delete buttons to task

##### simple-todos-angular.html

```html
[...]
  </header>

  <ul>
    <li ng-repeat="task in tasks" ng-class="{'checked': task.checked}">
      <button class="delete" ng-click="tasks.remove(task)">&times;</button>

      <input type="checkbox" ng-model="task.checked" class="toggle-checked" />

      <span class="text">{{task.text}}</span>
    </li>
  </ul>

</div>
[...]
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.html
diff --git a/simple-todos-angular/simple-todos-angular.html b/simple-todos-angular/simple-todos-angular.html
index 0c78c28..54c2196 100644
--- a/simple-todos-angular/simple-todos-angular.html
+++ b/simple-todos-angular/simple-todos-angular.html
@@ -19,7 +19,13 @@
     </header>

     <ul>
-      <li ng-repeat="task in tasks">{{task.text}}</li>
+      <li ng-repeat="task in tasks" ng-class="{'checked': task.checked}">
+        <button class="delete" ng-click="tasks.remove(task)">&times;</button>
+
+        <input class="toggle-checked" type="checkbox" ng-model="task.checked" />
+
+        <span class="text">{{task.text}}</span>
+      </li>
     </ul>

   </div>

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$
```

6. Deploying your app
---------------------

### Instructions

```sh
$ meteor deploy my_app_name.meteor.com
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ meteor deploy sho-simple-todos-angular.meteor.com
Deploying to sho-simple-todos-angular.meteor.com.
Now serving at http://sho-simple-todos-angular.meteor.com

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$
```

7. Running on mobile
--------------------

### Instructions

#### 7.1  Remove ng-app

##### simple-todos-angular.html

```html
[...]
<body>
<div class="container"
     ng-controller="TodosListCtrl">

  <header>
[...]
```

#### 7.2  Bootstrap Angular to mobile as well

##### simple-todos-angular.js

```javasscript
[...]
  // This code only runs on the client
  angular.module('simple-todos',['angular-meteor']);

  function onReady() {
    angular.bootstrap(document, ['simple-todos']);
  }

  if (Meteor.isCordova)
    angular.element(document).on('deviceready', onReady);
  else
    angular.element(document).ready(onReady);

  angular.module('simple-todos').controller('TodosListCtrl', ['$scope', '$meteor',
    function ($scope, $meteor) {
[...]
```

#### Running on an iOS simulator (Mac Only)

```sh
$ meteor install-sdk ios
$ meteor add-platform ios
$ meteor run ios
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.html
diff --git a/simple-todos-angular/simple-todos-angular.html b/simple-todos-angular/simple-todos-angular.html
index 54c2196..335adcd 100644
--- a/simple-todos-angular/simple-todos-angular.html
+++ b/simple-todos-angular/simple-todos-angular.html
@@ -4,7 +4,6 @@

 <body>
   <div class="container"
-       ng-app="simple-todos"
        ng-controller="TodosListCtrl">

     <header>
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.js
diff --git a/simple-todos-angular/simple-todos-angular.js b/simple-todos-angular/simple-todos-angular.js
index 722d230..61a1fa4 100644
--- a/simple-todos-angular/simple-todos-angular.js
+++ b/simple-todos-angular/simple-todos-angular.js
@@ -5,6 +5,15 @@ if (Meteor.isClient) {
   // This code only runs on the client
   angular.module('simple-todos',['angular-meteor']);

+  function onReady() {
+    angular.bootstrap(document, ['simple-todos']);
+  }
+
+  if (Meteor.isCordova)
+    angular.element(document).on('deviceready', onReady);
+  else
+    angular.element(document).ready(onReady);
+
   angular.module('simple-todos').controller('TodosListCtrl', ['$scope', '$meteor',
     function ($scope, $meteor) {
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ meteor install-sdk ios
Please follow the instructions here:
https://github.com/meteor/meteor/wiki/Mobile-Development-Install:-iOS-on-Mac

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ meteor add-platform ios
ios: added platform

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ meteor run ios
Can't listen on port 3000. Perhaps another Meteor is running?

Running two copies of Meteor in the same application directory
will not work. If something else is using port 3000, you can
specify an alternative port with --port <port>.
```

8. Filtering Collections
------------------------

### Instructions

#### 8.1  Add hideComplete checkbox to template

##### simple-todos-angular.html

```html
[...]
  <header>
    <h1>Todo List</h1>

    <label class="hide-completed">
      <input type="checkbox" ng-model="hideCompleted"/>
      Hide Completed Tasks
    </label>

    <!-- add a form below the h1 -->
    <form class="new-task" ng-submit="addTask(newTask); newTask='';">
      <input ng-model="newTask" type="text"
[...]
```

#### 8.2  Watch hideCompleted and change the query variable

##### simple-todos-angular.js

```javascript
[...]
        );
      };

      $scope.$watch('hideCompleted', function() {
        if ($scope.hideCompleted)
          $scope.query = {checked: {$ne: true}};
        else
          $scope.query = {};
      });

    }]);
}
```

#### 8.3  Change the Collection to use query parameter

##### simple-todos-angular.js

```javascript
[...]
  angular.module('simple-todos').controller('TodosListCtrl', ['$scope', '$meteor',
    function ($scope, $meteor) {

      $scope.tasks = $meteor.collection(function() {
        return Tasks.find($scope.query, {sort: {createdAt: -1}})
      });

      $scope.addTask = function (newTask) {
[...]
```

#### 8.4  Make query parameter reactive

##### simple-todos-angular.js

```javascript
[...]
    function ($scope, $meteor) {

      $scope.tasks = $meteor.collection(function() {
        return Tasks.find($scope.getReactively('query'), {sort: {createdAt: -1}})
      });

      $scope.addTask = function (newTask) {
[...]
```

#### 8.5  Add incompleteCount to scope

##### simple-todos-angular.js

```javascript
[...]
          $scope.query = {};
      });

      $scope.incompleteCount = function () {
        return Tasks.find({ checked: {$ne: true} }).count();
      };

    }]);
}
```

#### 8.6  Add incompleteCount to header

##### simple-todos-angular.html

```html
[...]
     ng-controller="TodosListCtrl">

  <header>
    <h1>Todo List ( {{ incompleteCount() }} )</h1>

    <label class="hide-completed">
      <input type="checkbox" ng-model="hideCompleted"/>
[...]
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.html
diff --git a/simple-todos-angular/simple-todos-angular.html b/simple-todos-angular/simple-todos-angular.html
index 335adcd..293d3ea 100644
--- a/simple-todos-angular/simple-todos-angular.html
+++ b/simple-todos-angular/simple-todos-angular.html
@@ -7,7 +7,12 @@
        ng-controller="TodosListCtrl">

     <header>
-      <h1>Todo List</h1>
+      <h1>Todo List ({{ incompleteCount() }})</h1>
+
+      <label class="hide-completed" for="">
+        <input type="checkbox" ng-model="hideCompleted"/>
+        Hide Completed Tasks
+      </label>

       <!-- add a form below the h1 -->
       <form class="new-task" ng-submit="addTask(newTask); newTask='';">
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.js
diff --git a/simple-todos-angular/simple-todos-angular.js b/simple-todos-angular/simple-todos-angular.js
index 61a1fa4..381f23b 100644
--- a/simple-todos-angular/simple-todos-angular.js
+++ b/simple-todos-angular/simple-todos-angular.js
@@ -18,7 +18,7 @@ if (Meteor.isClient) {
     function ($scope, $meteor) {

       $scope.tasks = $meteor.collection( function() {
-        return Tasks.find({}, { sort: { createdAt: -1 } })
+        return Tasks.find($scope.getReactively('query'), {sort: { createdAt: -1 }})
       });

       $scope.addTask = function (newTask) {
@@ -28,6 +28,17 @@ if (Meteor.isClient) {
         );
       };

+      $scope.$watch('hideCompleted', function() {
+        if ($scope.hideCompleted)
+          $scope.query = {checked: {$ne: true}};
+        else
+          $scope.query = {};
+      });
+
+      $scope.incompleteCount = function () {
+        return Tasks.find({ checked: {$ne: true} }).count();
+      };
+
   }]);
 }
```

9. Adding user accounts
-----------------------

### Instructions

To enable the accounts system and UI, we need to add the relevant packages. In your app directory, run the following command:

```sh
meteor add accounts-password dotansimha:accounts-ui-angular
```

#### 9.2  Add `accounts.ui` dependency to Angular app

##### simple-todos-angular.js

```javascript
[...]
if (Meteor.isClient) {

  // This code only runs on the client
  angular.module('simple-todos',['angular-meteor', 'accounts.ui']);

  function onReady() {
    angular.bootstrap(document, ['simple-todos']);
[...]
```

#### 9.3  Add loginButtons directive

##### simple-todos-angular.html

```html
[...]
      Hide Completed Tasks
    </label>

    <login-buttons></login-buttons>

    <!-- add a form below the h1 -->
    <form class="new-task" ng-submit="addTask(newTask); newTask='';">
      <input ng-model="newTask" type="text"
[...]
```

#### 9.4  Configure accounts UI to use usernames instead of email

##### simple-todos-angular.js

```javascript
[...]
if (Meteor.isClient) {

  Accounts.ui.config({
    passwordSignupFields: "USERNAME_ONLY"
  });

  // This code only runs on the client
  angular.module('simple-todos',['angular-meteor', 'accounts.ui']);
[...]
```

#### 9.5  Add owner and username to created task

##### simple-todos-angular.js

```javascript
[...]
        return Tasks.find($scope.getReactively('query'), {sort: {createdAt: -1}})
      });

      $scope.addTask = function(newTask) {
        $scope.tasks.push( {
            text: newTask,
            createdAt: new Date(),             // current time
            owner: Meteor.userId(),            // _id of logged in user
            username: Meteor.user().username }  // username of logged in user
        );
      };
[...]
```

#### 9.6  Hide new task form if user is not logged in

##### simple-todos-angular.html

```html
[...]
    <login-buttons></login-buttons>

    <!-- add a form below the h1 -->
    <form class="new-task"
          ng-submit="addTask(newTask); newTask='';"
          ng-show="$root.currentUser">
      <input ng-model="newTask" type="text"
             name="text" placeholder="Type to add new tasks" />
    </form>
[...]
```

#### 9.7  Add username to the displayed task

##### simple-todos-angular.html

```html
[...]
      <input type="checkbox" ng-model="task.checked" class="toggle-checked" />

      <span class="text">
        <strong>{{task.username}}</strong> - {{task.text}}
      </span>
    </li>
  </ul>
[...]
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ meteor add accounts-password dotansimha:accounts-ui-angular

Changes to your project's package version selections:

accounts-base                   added, version 1.2.2
accounts-password               added, version 1.1.4
accounts-ui                     added, version 1.1.6
accounts-ui-unstyled            added, version 1.1.8
blaze-html-templates            added, version 1.0.1
ddp-rate-limiter                added, version 1.0.0
dotansimha:accounts-ui-angular  added, version 0.0.2
email                           added, version 1.0.8
less                            added, version 2.5.1
localstorage                    added, version 1.0.5
npm-bcrypt                      added, version 0.7.8_2
rate-limit                      added, version 1.0.0
service-configuration           added, version 1.0.5
sha                             added, version 1.0.4
srp                             added, version 1.0.4
templating                      added, version 1.1.5


accounts-password: Password support for accounts
dotansimha:accounts-ui-angular: AngularJS wrapper for Meteor's Account-UI package
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.html
diff --git a/simple-todos-angular/simple-todos-angular.html b/simple-todos-angular/simple-todos-angular.html
index 293d3ea..d977e22 100644
--- a/simple-todos-angular/simple-todos-angular.html
+++ b/simple-todos-angular/simple-todos-angular.html
@@ -14,8 +14,12 @@
         Hide Completed Tasks
       </label>

+      <login-buttons></login-buttons>
+
       <!-- add a form below the h1 -->
-      <form class="new-task" ng-submit="addTask(newTask); newTask='';">
+      <form class="new-task"
+            ng-submit="addTask(newTask); newTask='';"
+            ng-show="$root.currentUser">
         <input ng-model="newTask" type="text"
                name="text" placeholder="Type to add new tasks" />
       </form>
@@ -28,7 +32,9 @@

         <input class="toggle-checked" type="checkbox" ng-model="task.checked" />

-        <span class="text">{{task.text}}</span>
+        <span class="text">
+          <strong>{{task.username}}</strong> - {{task.text}}
+        </span>
       </li>
     </ul>
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-angular on master [!]
$ git diff simple-todos-angular.js
diff --git a/simple-todos-angular/simple-todos-angular.js b/simple-todos-angular/simple-todos-angular.js
index 381f23b..0c8567b 100644
--- a/simple-todos-angular/simple-todos-angular.js
+++ b/simple-todos-angular/simple-todos-angular.js
@@ -2,8 +2,12 @@ Tasks = new Mongo.Collection('tasks');

 if (Meteor.isClient) {

+  Accounts.ui.config({
+    passwordSignupFields: "USERNAME_ONLY"
+  });
+
   // This code only runs on the client
-  angular.module('simple-todos',['angular-meteor']);
+  angular.module('simple-todos',['angular-meteor', 'accounts.ui']);

   function onReady() {
     angular.bootstrap(document, ['simple-todos']);
@@ -23,8 +27,10 @@ if (Meteor.isClient) {

       $scope.addTask = function (newTask) {
         $scope.tasks.push( {
-          text: newTask,
-          createdAt: new Date() }
+            text: newTask,
+            createdAt: new Date(),              // current time
+            owner: Meteor.userId(),             // _id of logged in user
+            username: Meteor.user().username }  // username of logged in user
         );
       };
```

10. Security with methods
-------------------------

### Instructions

### In my terminal emulator

```sh

```

11. Publish and subscribe
-------------------------

### Instructions

### In my terminal emulator

```sh

```

12. Next steps
--------------

### Instructions

### In my terminal emulator

```sh

```

