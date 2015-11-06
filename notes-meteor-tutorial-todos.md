Meteor Tutorial
===============

- [Meteor Tutorial](https://www.meteor.com/tutorials/blaze/creating-an-app) 

Creating your first app
-----------------------

To create the app, open your terminal and type:

```sh
meteor create simple-todos
```

```sh
Shoichi at sho-mbp in ~
$ meteor create simple-todos
Created a new Meteor app in 'simple-todos'.

To run your new app:
  cd simple-todos
  meteor

If you are new to Meteor, try some of the learning resources here:
  https://www.meteor.com/learn


Shoichi at sho-mbp in ~
$ cd simple-todos/

Shoichi at sho-mbp in ~/simple-todos
$ ls -alrthF
total 24
-rw-r--r--    1 Shoichi  staff   478B 23 Oct 16:32 simple-todos.js
-rw-r--r--    1 Shoichi  staff   225B 23 Oct 16:32 simple-todos.html
-rw-r--r--    1 Shoichi  staff    31B 23 Oct 16:32 simple-todos.css
drwxr-xr-x    6 Shoichi  staff   204B 23 Oct 16:32 ./
drwxr-xr-x   10 Shoichi  staff   340B 23 Oct 16:32 .meteor/
drwxr-xr-x+ 120 Shoichi  staff   4.0K 23 Oct 16:32 ../
```

### These tree files are created

##### `simple-todos.js`

```sh
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

##### `simple-todos.html`

```sh
<head>
  <title>simple-todos</title>
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

##### `simple-todos.css`

```
/* CSS declarations go here */
```

### To run the newly created app:

```sh
cd simple-todos
meteor
```

```sh
Shoichi at sho-mbp in ~
$ cd simple-todos/

Shoichi at sho-mbp in ~/simple-todos
$ meteor
[[[[[ ~/simple-todos ]]]]]

=> Started proxy.
=> Started MongoDB.
=> Started your app.

=> App running at: http://localhost:3000/

```

Open your web browser and go to `http://localhost:3000` to see the app running.

TODO![img](url)

### Run git init to track the tutorial project

```sh
Shoichi at sho-mbp in ~/simple-todos
$ git init
Initialized empty Git repository in /Users/Shoichi/simple-todos/.git/

Shoichi at sho-mbp in ~/simple-todos on master [?]
$ ls -alrthF
total 24
-rw-r--r--@   1 Shoichi  staff   478B 23 Oct 19:00 simple-todos.js
-rw-r--r--@   1 Shoichi  staff   225B 23 Oct 19:00 simple-todos.html
-rw-r--r--@   1 Shoichi  staff    31B 23 Oct 19:00 simple-todos.css
drwxr-xr-x@  10 Shoichi  staff   340B 23 Oct 19:00 .meteor/
drwxr-xr-x    9 Shoichi  staff   306B 23 Oct 19:13 .git/
drwxr-xr-x+ 123 Shoichi  staff   4.1K 23 Oct 19:13 ../
drwxr-xr-x@   7 Shoichi  staff   238B 23 Oct 19:13 ./
```

```sh
Shoichi at sho-mbp in ~/simple-todos on master [?]
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.meteor/
	simple-todos.css
	simple-todos.html
	simple-todos.js

nothing added to commit but untracked files present (use "git add" to track)

Shoichi at sho-mbp in ~/simple-todos on master [?]
$ git add .

Shoichi at sho-mbp in ~/simple-todos on master [+]
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   .meteor/.finished-upgraders
	new file:   .meteor/.gitignore
	new file:   .meteor/.id
	new file:   .meteor/packages
	new file:   .meteor/platforms
	new file:   .meteor/release
	new file:   .meteor/versions
	new file:   simple-todos.css
	new file:   simple-todos.html
	new file:   simple-todos.js


Shoichi at sho-mbp in ~/simple-todos on master [+]
$ git commit -m "Initial commit"
[master (root-commit) 8b3b355] Initial commit
 10 files changed, 147 insertions(+)
 create mode 100644 .meteor/.finished-upgraders
 create mode 100644 .meteor/.gitignore
 create mode 100644 .meteor/.id
 create mode 100644 .meteor/packages
 create mode 100644 .meteor/platforms
 create mode 100644 .meteor/release
 create mode 100644 .meteor/versions
 create mode 100644 simple-todos.css
 create mode 100644 simple-todos.html
 create mode 100644 simple-todos.js

Shoichi at sho-mbp in ~/simple-todos on master
$ git log --oneline --graph --decorate --all
* 8b3b355 (HEAD -> master) Initial commit
```

Defining views with templates
-----------------------------

### Replace starter HTML code

##### `simple-todos.html`

```html
<head>
  <title>Todo List</title>
</head>

<body>
  <div class="container">
    <header>
      <h1>Todo List</h1>
    </header>

    <ul>
      {{#each tasks}}
        {{> task}}
      {{/each}}
    </ul>
  </div>
</body>

<template name="task">
  <li>{{text}}</li>
</template>
```

### Replace starter JS code

##### `simple-todos.js`

```javascript
if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: [
      { text: "This is task 1" },
      { text: "This is task 2" },
      { text: "This is task 3" }
    ]
  });
}
```

In our browser, the app will now look much like this:

TODO![img](url)

### Replace simple-todos.css with this code

##### `simple-todos.css`

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
  background-image: linear-gradient(to bottom, #d03df5, #e1e5f0 100%);
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
  margin-height: 1em;
}

form {
  margin-top: 10px;
  margin-bottom: -10px;
  position: relative
}

.new-task input {
  box-sizing: border-box;
  padding: 10px 0;
  background: transparent;
  border: none;
  width: 100%
  padding-right: 80px;
  font-size: 1em;
}

.new-task input:focus {
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
  border-bottom: #eee splid 1px;
}

li .text {
  margin-left: 10px;
}

li.checked .text {
  color: #888;
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

Now the app has been styled by CSS

TODO![img](url)

### Run `git commit`

```sh
Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git st
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   simple-todos.css
	modified:   simple-todos.html
	modified:   simple-todos.js

no changes added to commit (use "git add" and/or "git commit -a")

Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git commit -am "Add the given code to html, css and js files"
[master 51efff2] Add the given code to html, css and js files
 3 files changed, 159 insertions(+), 32 deletions(-)
 rewrite simple-todos.js (93%)

Shoichi at sho-mbp in ~/simple-todos on master
$ git status
On branch master
nothing to commit, working directory clean

Shoichi at sho-mbp in ~/simple-todos on master
$ git log --oneline --graph --decorate --all
* 51efff2 (HEAD -> master) Add the given code to html, css and js files
* 8b3b355 Initial commit
```

Storing tasks in a collection
-----------------------------

### Define Tasks collection and load tasks from it

Let's update our JavaScript code to get our tasks from a collection instead of a static array:

##### `simple-todos.js`

```javascript
Tasks = new Mongo.Collection("tasks");

if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: function() {
      return Tasks.find({});
    }
  });
}
```

```sh
Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git diff
diff --git a/simple-todos.js b/simple-todos.js
index a935bb9..de0ba09 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -1,11 +1,11 @@
+Tasks = new Mongo.Collection("tasks");
+
 if (Meteor.isClient) {
   // This code only runs on the client
   Template.body.helpers({
-    tasks: [
-      { text: "This is task 1" },
-      { text: "This is task 2" },
-      { text: "This is task 3" }
-    ]
+    tasks: function() {
+      return Tasks.find({});
+    }
   });
 }
```

### Inserting tasks from the console

```sh
Shoichi at sho-mbp in ~/simple-todos
$ meteor mongo
MongoDB shell version: 2.6.7
connecting to: 127.0.0.1:3001/meteor
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
	http://docs.mongodb.org/
Questions? Try the support group
	http://groups.google.com/group/mongodb-user
meteor:PRIMARY> db.tasks.insert({ text: "Hello world!", createdAt: new Date() });
WriteResult({ "nInserted" : 1 })
meteor:PRIMARY>
```

Adding tasks with a form
------------------------

### Add form for new tasks

##### `simple-todos.html`

```html
<head>
  <title>Todo List</title>
</head>

<body>
  <div class="container">
    <header>
      <h1>Todo List</h1>

      <form class="new-task" action="">
        <input type="text" name="text" placeholder="Type to add new tasks" />
      </form>
    </header>

    <ul>
      {{#each tasks}}
        {{> task}}
      {{/each}}
    </ul>
  </div>
</body>

<template name="task">
  <li>{{text}}</li>
</template>
```

### Add event handler for form submit

##### `simple-todos.js`

```javascript
Tasks = new Mongo.Collection("tasks");

if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: function() {
      return Tasks.find({});
    }
  });

  Template.body.events({
    "submit .new-task": function (event) {
      // Prevent default browser from submit
      event.preventDefault();

      // Get value from form element
      var text = event.target.text.value;

      // Insert a task into the collection
      Tasks.insert({
        text: text,
        createdAt: new Date() // current time
      });

      // Clear form
      event.target.text.value = "";
    }
  });
}
```

### Run `git commit`

```sh
Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   simple-todos.html
	modified:   simple-todos.js

no changes added to commit (use "git add" and/or "git commit -a")

Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git add simple-todos.html

Shoichi at sho-mbp in ~/simple-todos on master [+!]
$ git commit -m "Add input form for new tasks"
[master db7e1f1] Add input form for new tasks
 1 file changed, 7 insertions(+), 3 deletions(-)

Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   simple-todos.js

no changes added to commit (use "git add" and/or "git commit -a")

Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git add simple-todos.js

Shoichi at sho-mbp in ~/simple-todos on master [+]
$ git commit -m "Add event hundler for form submit"
[master 99b09d4] Add event hundler for form submit
 1 file changed, 19 insertions(+)

Shoichi at sho-mbp in ~/simple-todos on master
$ git log --oneline --graph --decorate --all
* 99b09d4 (HEAD -> master) Add event hundler for form submit
* db7e1f1 Add input form for new tasks
* f8adefd Define Tasks collection and load tasks from it
* 51efff2 Add the given code to html, css and js files
* 8b3b355 Initial commit
```

### Show newest tasks at the top

##### simple-todos.js

```javascript
Tasks = new Mongo.Collection("tasks");

if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: function() {
      // Show newest tasks at the top
      return Tasks.find({}, {sort: {createdAt: -1}});
    }
  });

  Template.body.events({
    "submit .new-task": function (event) {
      // Prevent default browser form submit
      event.preventDefault();

      // Get value from form element
      var text = event.target.text.value;

      // Insert a task into the collection
      Tasks.insert({
        text: text,
        createdAt: new Date() // current time
      });

      // Clear form
      event.target.text.value = "";
    }
  });
}
```

```javascript
if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: function() {
-     return Tasks.find({});
+     // Show newest tasks at the top
+     return Tasks.find({}, {sort: {createdAt: -1}});
    }
  });
```

### Run `git commit`

```sh
Shoichi at sho-mbp in ~/simple-todos on master
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   simple-todos.js

no changes added to commit (use "git add" and/or "git commit -a")

Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git commit -am "Show newest tasks at the top"
[master 0d8ac41] Show newest tasks at the top
 1 file changed, 2 insertions(+), 1 deletion(-)

Shoichi at sho-mbp in ~/simple-todos on master
$ git log --oneline --graph --decorate --all
* 0d8ac41 (HEAD -> master) Show newest tasks at the top
* 99b09d4 Add event hundler for form submit
* db7e1f1 Add input form for new tasks
* f8adefd Define Tasks collection and load tasks from it
* 51efff2 Add the given code to html, css and js files
* 8b3b355 Initial commit
```

Checking off and deleting tasks
-------------------------------

### Add buttons to Task component

##### `simple-todos.html`

```html
<head>
  <title>Todo List</title>
</head>

<body>
  <div class="container">
    <header>
      <h1>Todo List</h1>

      <form class="new-task">
        <input type="text" name="text" placeholder="Type to add new tasks" />
      </form>
    </header>

    <ul>
      {{#each tasks}}
        {{> task}}
      {{/each}}
    </ul>
  </div>
</body>

<template name="task">
  <li class="{{#if checked}}checked{{/if}}">
    <button class="delete">&times;</button>

    <input type="checkbox" checked="{{checked}}" class="toggle-checked" />

    <span class="text">{{text}}</span>
  </li>
</template>
```

```sh
diff --git a/simple-todos.html b/simple-todos.html
index e31aef1..94341cc 100644
--- a/simple-todos.html
+++ b/simple-todos.html
@@ -21,5 +21,11 @@
 </body>
 
 <template name="task">
-  <li>{{text}}</li>
+  <li class="{{#if checked}}checked{{/if}}">
+    <button class="delete">&times;</button>
+
+    <input type="checkbox" checked="{{checked}}" class="toggle-checked" />
+
+    <span class="text">{{text}}</span>
+  </li>
 </template>
```

### Add event handlers for Task buttons

##### `simple-todos.js`

```javascript
Tasks = new Mongo.Collection("tasks");

if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: function() {
      // Show newest tasks at the top
      return Tasks.find({}, {sort: {createdAt: -1}});
    }
  });

  Template.body.events({
    "submit .new-task": function (event) {
      // Prevent default browser form submit
      event.preventDefault();

      // Get value from form element
      var text = event.target.text.value;

      // Insert a task into the collection
      Tasks.insert({
        text: text,
        createdAt: new Date() // current time
      });

      // Clear form
      event.target.text.value = "";
    }
  });

  Template.task.events({
    "click .toggle-checked": function () {
      // Set the checked property to the opposite of its current value
      Tasks.update(this._id, {
        $set: {checked: ! this.checked}
      });
    },
    "click .delete": function () {
      Tasks.remove(this._id);
    }
  });
}
```

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 5941766..19f0109 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -27,6 +27,18 @@ if (Meteor.isClient) {
       event.target.text.value = "";
     }
   });
+
+  Template.task.events({
+    "click .toggle-checked": function () {
+      // Set the checked property to the opposite of its current value
+      Tasks.update(this._id, {
+        $set: {checked: ! this.checked}
+      });
+    },
+    "click .delete": function () {
+      Tasks.remove(this._id);
+    }
+  });
 }
 
 /*
```

### Run `git commit`

```sh
Shoichi at sho-mbp in ~/simple-todos on master [!?]
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   simple-todos.html
	modified:   simple-todos.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	notes-meteor-tutorial-todos.md

no changes added to commit (use "git add" and/or "git commit -a")

Shoichi at sho-mbp in ~/simple-todos on master [!?]
$ git add notes-meteor-tutorial-todos.md

Shoichi at sho-mbp in ~/simple-todos on master [+!]
$ git commit -m "Add my personal notes for simple-todos app tutorial"
[master 987bf11] Add my personal notes for simple-todos app tutorial
 1 file changed, 819 insertions(+)
 create mode 100644 notes-meteor-tutorial-todos.md

Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git commit -am "Add delete buttons and its event hundlers"
[master 1e18505] Add delete buttons and its event hundlers
 2 files changed, 19 insertions(+), 1 deletion(-)

Shoichi at sho-mbp in ~/simple-todos on master
$ git log --oneline --graph --decorate --all
* 1e18505 (HEAD -> master) Add delete buttons and its event hundlers
* 987bf11 Add my personal notes for simple-todos app tutorial
* 0d8ac41 Show newest tasks at the top
* 99b09d4 Add event hundler for form submit
* db7e1f1 Add input form for new tasks
* f8adefd Define Tasks collection and load tasks from it
* 51efff2 Add the given code to html, css and js files
* 8b3b355 Initial commit
```

Deploying your app
------------------

```sh
Shoichi at sho-mbp in ~/simple-todos on master [!]
$ meteor deploy sho-simple-todos.meteor.com
To instantly deploy your app on a free testing server, just enter your email address!
Email: example@domain.com

Deploying to sho-simple-todos.meteor.com.
                                               Minifying app code                         Now serving at http://sho-simple-todos.meteor.com

You should set a password on your Meteor developer account. It takes about a minute at:
https://www.meteor.com/setPassword?F85mevBaMZ
```

Running your app on Android or iOS
----------------------------------

### Running on an iOS simulator (Mac Only)

```sh
Shoichi at sho-mbp in ~/simple-todos on master [!]
$ meteor install-sdk ios
Please follow the instructions here:
https://github.com/meteor/meteor/wiki/Mobile-Development-Install:-iOS-on-Mac

Shoichi at sho-mbp in ~/simple-todos on master [!]
$ meteor add-platform ios
ios: added platform

Shoichi at sho-mbp in ~/simple-todos on master [!]
$ meteor run ios
[[[[[ ~/simple-todos ]]]]]

=> Started proxy.
=> Started MongoDB.
=> Started your app.

=> App running at: http://localhost:3000/
=> Started app on iOS Simulator.
```

Storing temporary UI state in Session
-------------------------------------

### Add hide-completed checkbox to HTML

##### `simple-todos.html`

```html
<head>
  <title>Todo List</title>
</head>

<body>
  <div class="container">
    <header>
      <h1>Todo List</h1>

      <label class="hide-completed">
        <input type="checkbox" checked="{{hideCompleted}}" />
        Hide Completed Tasks
      </label>

      <form class="new-task">
        <input type="text" name="text" placeholder="Type to add new tasks" />
      </form>
    </header>

    <ul>
      {{#each tasks}}
        {{> task}}
      {{/each}}
    </ul>
  </div>
</body>

<template name="task">
  <li class="{{#if checked}}checked{{/if}}">
    <button class="delete">&times;</button>

    <input type="checkbox" checked="{{checked}}" class="toggle-checked" />

    <span class="text">{{text}}</span>
  </li>
</template>
```


```sh
Shoichi at sho-mbp in ~/simple-todos on master [!]
$ git diff simple-todos.html
diff --git a/simple-todos.html b/simple-todos.html
index 94341cc..7d837a9 100644
--- a/simple-todos.html
+++ b/simple-todos.html
@@ -7,6 +7,11 @@
     <header>
       <h1>Todo List</h1>

+      <label class="hide-completed">
+        <input type="checkbox" checked="{{hideCompleted}}" />
+        Hide Completed Tasks
+      </label>
+
       <form class="new-task">
         <input type="text" name="text" placeholder="Type to add new tasks" />
       </form>
```

### Add event handler for checkbox

##### `simple-todos.js`

```javascript
Tasks = new Mongo.Collection("tasks");

if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: function() {
      if (Session.get("hideCompleted")) {
        // If hide completed is checked, filter tasks
        return Tasks.find({checked: {$ne: true}}, {sort: {createdAt: -1}});
      } else {
        // Otherwise, return all of the tasks
        return Tasks.find({}, {sort: {createdAt: -1}});
      }
    },
    hideCompleted: function () {
      return Session.get("hideCompleted");
    }
  });

  Template.body.events({
    "submit .new-task": function (event) {
      // Prevent default browser form submit
      event.preventDefault();

      // Get value from form element
      var text = event.target.text.value;

      // Insert a task into the collection
      Tasks.insert({
        text: text,
        createdAt: new Date() // current time
      });

      // Clear form
      event.target.text.value = "";
    },
    "change .hide-completed input": function (event) {
      Session.set("hideCompleted", event.target.checked);
    }
  });

  Template.task.events({
    "click .toggle-checked": function () {
      // Set the checked property to the opposite of its current value
      Tasks.update(this._id, {
        $set: {checked: ! this.checked}
      });
    },
    "click .delete": function () {
      Tasks.remove(this._id);
    }
  });
}

/*
 * if (Meteor.isServer) {
 *   Meteor.startup(function () {
 *     // code to run on server at startup
 *   });
 * }
 */
```

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 19f0109..a6fedee 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -4,8 +4,16 @@ if (Meteor.isClient) {
   // This code only runs on the client
   Template.body.helpers({
     tasks: function() {
-      // Show newest tasks at the top
-      return Tasks.find({}, {sort: {createdAt: -1}});
+      if (Session.get("hideCompleted")) {
+        // If hide completed is checked, filter tasks
+        return Tasks.find({checked: {$ne: true}}, {sort: {createdAt: -1}});
+      } else {
+        // Otherwise, return all of the tasks
+        return Tasks.find({}, {sort: {createdAt: -1}});
+      }
+    },
+    hideCompleted: function () {
+      return Session.get("hideCompleted");
     }
   });
 
@@ -25,6 +33,9 @@ if (Meteor.isClient) {
 
       // Clear form
       event.target.text.value = "";
+    },
+    "change .hide-completed input": function (event) {
+      Session.set("hideCompleted", event.target.checked);
     }
   });
```

### Add incompleteCount helper to body

##### `simple-todos.js`

```javascript
Tasks = new Mongo.Collection("tasks");

if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: function() {
      if (Session.get("hideCompleted")) {
        // If hide completed is checked, filter tasks
        return Tasks.find({checked: {$ne: true}}, {sort: {createdAt: -1}});
      } else {
        // Otherwise, return all of the tasks
        return Tasks.find({}, {sort: {createdAt: -1}});
      }
    },
    hideCompleted: function () {
      return Session.get("hideCompleted");
    },
    incompleteCount: function () {
      return Tasks.find({checked: {$ne: true}}).count();
    }
  });

  Template.body.events({
    "submit .new-task": function (event) {
      // Prevent default browser form submit
      event.preventDefault();

      // Get value from form element
      var text = event.target.text.value;

      // Insert a task into the collection
      Tasks.insert({
        text: text,
        createdAt: new Date() // current time
      });

      // Clear form
      event.target.text.value = "";
    },
    "change .hide-completed input": function (event) {
      Session.set("hideCompleted", event.target.checked);
    }
  });

  Template.task.events({
    "click .toggle-checked": function () {
      // Set the checked property to the opposite of its current value
      Tasks.update(this._id, {
        $set: {checked: ! this.checked}
      });
    },
    "click .delete": function () {
      Tasks.remove(this._id);
    }
  });
}

/*
 * if (Meteor.isServer) {
 *   Meteor.startup(function () {
 *     // code to run on server at startup
 *   });
 * }
 */
```


```sh
diff --git a/simple-todos.js b/simple-todos.js
index a6fedee..a9c5406 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -14,6 +14,9 @@ if (Meteor.isClient) {
     },
     hideCompleted: function () {
       return Session.get("hideCompleted");
+    },
+    incompleteCount: function () {
+      return Tasks.find({checked: {$ne: true}}).count();
     }
   });
```

### Display incompleteCount

##### `simple-todos.js`

```html
<head>
  <title>Todo List</title>
</head>

<body>
  <div class="container">
    <header>
      <h1>Todo List ({{incompleteCount}})</h1>

      <label class="hide-completed">
        <input type="checkbox" checked="{{hideCompleted}}" />
        Hide Completed Tasks
      </label>

      <form class="new-task">
        <input type="text" name="text" placeholder="Type to add new tasks" />
      </form>
    </header>

    <ul>
      {{#each tasks}}
        {{> task}}
      {{/each}}
    </ul>
  </div>
</body>

<template name="task">
  <li class="{{#if checked}}checked{{/if}}">
    <button class="delete">&times;</button>

    <input type="checkbox" checked="{{checked}}" class="toggle-checked" />

    <span class="text">{{text}}</span>
  </li>
</template>
```

```sh
diff --git a/simple-todos.html b/simple-todos.html
index 7d837a9..cb9b6f1 100644
--- a/simple-todos.html
+++ b/simple-todos.html
@@ -5,7 +5,7 @@
 <body>
   <div class="container">
     <header>
-      <h1>Todo List</h1>
+      <h1>Todo List ({{incompleteCount}})</h1>
 
       <label class="hide-completed">
         <input type="checkbox" checked="{{hideCompleted}}" />
```

Adding user accounts
--------------------

```sh
$ meteor add accounts-ui accounts-password
```

```sh
Shoichi at sho-mbp in ~/simple-todos on master
$ meteor add accounts-ui accounts-password

Changes to your project's package version selections:

accounts-base          added, version 1.2.1
accounts-password      added, version 1.1.3
accounts-ui            added, version 1.1.6
accounts-ui-unstyled   added, version 1.1.8
ddp-rate-limiter       added, version 1.0.0
email                  added, version 1.0.7
less                   added, version 2.5.0_3
localstorage           added, version 1.0.5
npm-bcrypt             added, version 0.7.8_2
rate-limit             added, version 1.0.0
service-configuration  added, version 1.0.5
sha                    added, version 1.0.4
srp                    added, version 1.0.4


accounts-ui: Simple templates to add login widgets to an app
accounts-password: Password support for accounts
```

### Include loginButtons

```sh
diff --git a/simple-todos.html b/simple-todos.html
index cb9b6f1..55f385c 100644
--- a/simple-todos.html
+++ b/simple-todos.html
@@ -12,6 +12,8 @@
         Hide Completed Tasks
       </label>
 
+      {{> loginButtons}}
+
       <form class="new-task">
         <input type="text" name="text" placeholder="Type to add new tasks" />
       </form>
```

### Configure accounts-ui

```sh
diff --git a/simple-todos.js b/simple-todos.js
index a9c5406..50ee1c1 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -53,6 +53,10 @@ if (Meteor.isClient) {
       Tasks.remove(this._id);
     }
   });
+
+  Acconts.ui.config({
+    passwordSignupFields: "USERNAME_ONLY"
+  });
 }
```

### Update insert to include user data

```sh
diff --git a/simple-todos.js b/simple-todos.js
index a9c5406..21da329 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -31,7 +31,9 @@ if (Meteor.isClient) {
       // Insert a task into the collection
       Tasks.insert({
         text: text,
-        createdAt: new Date() // current time
+        createdAt: new Date(),            // current time
+        owner: Meteor.userId(),           // _id of logged in user
+        username: Meteor.user().username  // username of logged in user
       });
 
       // Clear form
```

### Only show add task form if logged in

```sh
diff --git a/simple-todos.html b/simple-todos.html
index cb9b6f1..9e4b61a 100644
--- a/simple-todos.html
+++ b/simple-todos.html
@@ -12,9 +12,13 @@
         Hide Completed Tasks
       </label>
 
-      <form class="new-task">
-        <input type="text" name="text" placeholder="Type to add new tasks" />
-      </form>
+      {{> loginButtons}}
+
+      {{#if currentUser}}
+        <form class="new-task">
+          <input type="text" name="text" placeholder="Type to add new tasks" />
+        </form>
+      {{/if}}
     </header>
 
     <ul>
```

### Display username next to task

```sh
diff --git a/simple-todos.html b/simple-todos.html
index cb9b6f1..55c1dc9 100644
--- a/simple-todos.html
+++ b/simple-todos.html
[...]
@@ -31,6 +35,6 @@
 
     <input type="checkbox" checked="{{checked}}" class="toggle-checked" />
 
-    <span class="text">{{text}}</span>
+    <span class="text"><strong>{{username}}</strong> - {{text}}</span>
   </li>
 </template>
```

Security with methods
---------------------

### Removing the `insecure` pacakage

```sh
$ meteor remove insecure
```

```sh
Shoichi at sho-mbp in ~/simple-todos on master
$ meteor remove insecure

Changes to your project's package version selections:

insecure  removed from your project

insecure: removed dependency
```

### Define some methods

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 21da329..4994205 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -61,6 +61,28 @@ if (Meteor.isClient) {
   });
 }
 
+Meteor.methods({
+  addTask: function (text) {
+    // Make sure the user is logged in before inserting a task
+    if (! Meteor.userId()) {
+      throw new Meteor.Error("not-authorized");
+    }
+
+    Tasks.insert({
+      text: text,
+      createdAt: new Date(),            // current time
+      owner: Meteor.userId(),           // _id of logged in user
+      username: Meteor.user().username  // username of logged in user
+    });
+  },
+  deleteTask: function (taskId) {
+    Tasks.remove(taskId);
+  },
+  setChecked: function (taskId, setChecked) {
+    Tasks.update(taskId, { $set: { checked: setChecked} });
+  }
+});
+
```

### Replace insert with addTask method

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 21da329..f2271f8 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -29,12 +29,7 @@ if (Meteor.isClient) {
       var text = event.target.text.value;
 
       // Insert a task into the collection
-      Tasks.insert({
-        text: text,
-        createdAt: new Date(),            // current time
-        owner: Meteor.userId(),           // _id of logged in user
-        username: Meteor.user().username  // username of logged in user
-      });
+      Meteor.call("addTask", text);
 
       // Clear form
       event.target.text.value = "";
[...]
```

### Replace update and remove with methods

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 21da329..61f86de 100644
--- a/simple-todos.js
+++ b/simple-todos.js
[...]
@@ -47,12 +42,10 @@ if (Meteor.isClient) {
   Template.task.events({
     "click .toggle-checked": function () {
       // Set the checked property to the opposite of its current value
-      Tasks.update(this._id, {
-        $set: {checked: ! this.checked}
-      });
+      Meteor.call("setChecked", this._id, ! this.checked);
     },
     "click .delete": function () {
-      Tasks.remove(this._id);
+      Meteor.call("deleteTask", this._id);
     }
   });
[...]
```

Filtering data with publish and subscribe
-----------------------------------------

### Remove default `autopublish` package

```sh
$ meteor remove autopublish
```

```sh
Shoichi at sho-mbp in ~/simple-todos on master [!]
$ meteor remove autopublish

Changes to your project's package version selections:

autopublish  removed from your project

autopublish: removed dependency
```

### Add publish and subscribe

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 61f86de..5f72159 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -1,7 +1,16 @@
 Tasks = new Mongo.Collection("tasks");
 
+if (Meteor.isServer) {
+  // This code only runs on the server
+  Meteor.publish("tasks", function () {
+    return Tasks.find();
+  });
+}
+
 if (Meteor.isClient) {
   // This code only runs on the client
+  Meteor.subscribe("tasks");
+
   Template.body.helpers({
     tasks: function() {
       if (Session.get("hideCompleted")) {
```

### Add private button

```sh
diff --git a/simple-todos.html b/simple-todos.html
index 55c1dc9..94372b0 100644
--- a/simple-todos.html
+++ b/simple-todos.html
@@ -35,6 +35,16 @@
 
     <input type="checkbox" checked="{{checked}}" class="toggle-checked" />
 
+    {{#if isOwner}}
+      <button class="toggle-private">
+        {{#if private}}
+          Private
+        {{else}}
+          Public
+        {{/if}}
+      </button>
+    {{/if}}
+
     <span class="text"><strong>{{username}}</strong> - {{text}}</span>
   </li>
 </template>
```

### Add private class to private tasks

```sh
diff --git a/simple-todos.html b/simple-todos.html
index 55c1dc9..5e2af69 100644
--- a/simple-todos.html
+++ b/simple-todos.html
@@ -30,11 +30,21 @@
 </body>
 
 <template name="task">
-  <li class="{{#if checked}}checked{{/if}}">
+  <li class="{{#if checked}}checked{{/if}} {{#if private}}private{{/if}}">
     <button class="delete">&times;</button> 
[...]
```

### Define helper to check ownership

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 61f86de..c361e80 100644
--- a/simple-todos.js
+++ b/simple-todos.js
[...]
@@ -39,6 +48,12 @@ if (Meteor.isClient) {
     }
   });
 
+  Template.task.helpers({
+    isOwner: function () {
+      return this.owner === Meteor.userId();
+    }
+  });
+
   Template.task.events({
     "click .toggle-checked": function () {
       // Set the checked property to the opposite of its current value
```

### Define method to set tasks to private

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 61f86de..d5f1de9 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -1,7 +1,16 @@
[...]
@@ -73,6 +88,16 @@ Meteor.methods({
   },
   setChecked: function (taskId, setChecked) {
     Tasks.update(taskId, { $set: { checked: setChecked} });
+  },
+  setPrivate: function (taskId, setToPrivate) {
+    var task = Tasks.findOne(taskId);
+
+    // Make sure only the task owner can make a task private
+    if (task.owner !== Meteor.userId()) {
+      throw new Meteor.Error("not-authorized");
+    }
+
+    Tasks.update(taskId, { $set: { private: setToPrivate } });
   }
 });
```

### Add event handler to call the setPrivate method

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 61f86de..fc6afb4 100644
--- a/simple-todos.js
+++ b/simple-todos.js
[...]
@@ -46,6 +61,9 @@ if (Meteor.isClient) {
     },
     "click .delete": function () {
       Meteor.call("deleteTask", this._id);
+    },
+    "click .toggle-private": function () {
+      Meteor.call("setPrivate", this._id, ! this.private);
     }
   });
 
[...]
```

### Only publish tasks the user is allowed to see

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 61f86de..c7ddee8 100644
--- a/simple-todos.js
+++ b/simple-todos.js
@@ -1,7 +1,22 @@
 Tasks = new Mongo.Collection("tasks");
 
+if (Meteor.isServer) {
+  // This code only runs on the server
+  // Only publish tasks that are public or belog to the current user
+  Meteor.publish("tasks", function () {
+    return Tasks.find({
+      $or: [
+        { private: {$ne: true} },
+        { owner: this.userId }
+      ]
+    });
+  });
+}
+
[...]
```

### Add some extra security to methods

```sh
diff --git a/simple-todos.js b/simple-todos.js
index 61f86de..c39c10c 100644
--- a/simple-todos.js
+++ b/simple-todos.js
[...] 
@@ -69,10 +93,32 @@ Meteor.methods({
     });
   },
   deleteTask: function (taskId) {
+    var task = Tasks.findOne(taskId);
+    if (task.private && task.owner !== Meteor.userId()) {
+      // If the task is private, make sure only the owner can delete it
+      throw new Meteor.Error("not-authorized");
+    }
+
     Tasks.remove(taskId);
   },
   setChecked: function (taskId, setChecked) {
+    var task = Tasks.findOne(taskId);
+    if (task.private && task.owner !== Meteor.userId()) {
+      // If the task is private, make sure only the owner can check it off
+      throw new Meteor.Error("not-authorized");
+    }
+
     Tasks.update(taskId, { $set: { checked: setChecked} });
[...]
```

