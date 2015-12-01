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

Open a new terminal in the same directory as your running app, and type:

```sh
$ meteor add react
```

#### Replace the starter code

To get started, let's replace the code of the default starter app. Then we'll talk about what it does.

First, replace the content of the initial HTML file:

#### 2.2  Replace starter HTML code

##### `simple-todos-react.html`

```html
<head>
  <title>Todo List</title>
</head>

<body>
  <div id="render-target"></div>
</body>
```

Second, delete simple-todos-react.js and create three new files:

#### 2.3  Replace starter JS

##### `simple-todos-react.jsx`

```javascript
if (Meteor.isClient) {
  // This code is executed on the client only

  Meteor.startup(function () {
    // Use Meteor.startup to render the component after the page is ready
    React.render(<App />, document.getElementById("render-target"));
  });
}
```

#### 2.4  Create App component

##### `App.jsx`

```javascript
// App component - represents the whole app
App = React.createClass({
  getTasks() {
    return [
      { _id: 1, text: "This is task 1" },
      { _id: 2, text: "This is task 2" },
      { _id: 3, text: "This is task 3" }
    ];
  },

  renderTasks() {
    return this.getTasks().map((task) => {
      return <Task key={task._id} task={task} />;
    });
  },

  render() {
    return (
      <div className="container">
        <header>
          <h1>Todo List</h1>
        </header>

        <ul>
          {this.renderTasks()}
        </ul>
      </div>
    );
  }
});
```

#### 2.5  Create Task component

##### `Task.jsx`

```javascript
// Task component - represents a single todo item
Task = React.createClass({
  propTypes: {
    // This component gets the task to display through a React prop.
    // We can use propTypes to indicate it is required
    task: React.PropTypes.object.isRequired
  },
  render() {
    return (
      <li>{this.props.task.text}</li>
    );
  }
});
```

#### Add the given CSS template

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
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master
$ meteor add react

Changes to your project's package version
selections:

coffeescript        added, version 1.0.11
cosmos:browserify   added, version 0.8.4
jsx                 added, version 0.2.3
react               added, version 0.14.1_1
react-meteor-data   added, version 0.2.3
react-runtime       added, version 0.14.1_1
react-runtime-dev   added, version 0.14.1
react-runtime-prod  added, version 0.14.1


react: Everything you need to use React
with Meteor.
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [+!?]
$ git diff simple-todos-react.html
diff --git a/simple-todos-react/simple-todos-react.html b/simple-todos-react/simple-todos-react.html
index e296a58..1aae2d4 100644
--- a/simple-todos-react/simple-todos-react.html
+++ b/simple-todos-react/simple-todos-react.html
@@ -1,14 +1,7 @@
 <head>
-  <title>simple-todos-react</title>
+  <title>Todo List</title>
 </head>

 <body>
-  <h1>Welcome to Meteor!</h1>
-
-  {{> hello}}
+  <div id="render-target"></div>
 </body>
-
-<template name="hello">
-  <button>Click Me</button>
-  <p>You've pressed the button {{counter}} times.</p>
-</template>
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [+!?]
$ git diff simple-todos-react.jsx
diff --git a/simple-todos-react/simple-todos-react.jsx b/simple-todos-react/simple-todos-react.jsx
index 4f8c65d..a7e2d2f 100644
--- a/simple-todos-react/simple-todos-react.jsx
+++ b/simple-todos-react/simple-todos-react.jsx
@@ -1,23 +1,8 @@
 if (Meteor.isClient) {
-  // counter starts at 0
-  Session.setDefault('counter', 0);
+  // This code is executed on the client only

-  Template.hello.helpers({
-    counter: function () {
-      return Session.get('counter');
-    }
-  });
-
-  Template.hello.events({
-    'click button': function () {
-      // increment the counter when button is clicked
-      Session.set('counter', Session.get('counter') + 1);
-    }
-  });
-}
-
-if (Meteor.isServer) {
   Meteor.startup(function () {
-    // code to run on server at startup
+    // Use Meteor.startup to render the component after the page is ready
+    React.render(<App />, document.getElementById("render-target"));
   });
 }
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [+]
$ git diff --staged App.jsx
diff --git a/simple-todos-react/App.jsx b/simple-todos-react/App.jsx
new file mode 100644
index 0000000..0d85460
--- /dev/null
+++ b/simple-todos-react/App.jsx
@@ -0,0 +1,30 @@
+// App component - represents the whole app
+App = React.createClass({
+  getTasks() {
+    return [
+      { _id: 1, text: "This is task 1" },
+      { _id: 2, text: "This is task 3" },
+      { _id: 3, text: "This is task 3" }
+    ];
+  },
+
+  renderTasks() {
+    return this.getTasks().map((task) => {
+      return <Task key={task._id} task={task} />
+    });
+  },
+
+  render() {
+    return (
+      <div className="container">
+        <header>
+          <h1>Todo List</h1>
+        </header>
+
+        <ul>
+          {this.renderTasks()}
+        </ul>
+      </div>
+    );
+  }
+});
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [+]
$ git diff --staged Task.jsx
diff --git a/simple-todos-react/Task.jsx b/simple-todos-react/Task.jsx
new file mode 100644
index 0000000..c49e7ac
--- /dev/null
+++ b/simple-todos-react/Task.jsx
@@ -0,0 +1,13 @@
+// Task component - represents a single todo item
+Task = React.createClass({
+  propTypes: {
+    // This component gets the task to display through a React prop.
+    // We can use propTypes to indicate it is required
+    task: React.PropTypes.object.isRequired
+  },
+  render() {
+    return (
+      <li>{this.props.task.text}</li>
+    );
+  }
+});
```

3. Collections
--------------

### Instructions

Let's add a line of code to define our first collection:

#### 3.1  Define tasks collection

##### `simple-todos-react.jsx`

```javascript
// Define a collection to hold our tasks
Tasks = new Mongo.Collection("tasks");

if (Meteor.isClient) {
  // This code is executed on the client only
[...]
```

#### Using data from a collection inside a React component

To use data from a Meteor collection inside a React component, include the `ReactMeteorData` mixin in a component. With this mixin in your component, you can define a method called `getMeteorData` which knows how to keep track of changes in data. The object you return from `getMeteorData` can be accessed on `this.data` inside the `render` method. Let's do this now:

#### 3.2  Modify App component to get tasks from collection

##### `App.jsx`

```javascript
// App component - represents the whole app
App = React.createClass({

  // This mixin makes the getMeteorData method work
  mixins: [ReactMeteorData],

  // Loads items from the Tasks collection and puts them on this.data.tasks
  getMeteorData() {
    return {
      tasks: Tasks.find({}).fetch()
    }
  },

  renderTasks() {
    // Get tasks from this.data.tasks
    return this.data.tasks.map((task) => {
      return <Task key={task._id} task={task} />;
    });
  },
[...]
```

When you make these changes to the code, you'll notice that the tasks that used to be in the todo list have disappeared. That's because our database is currently empty — we need to insert some tasks!

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [!]
$ meteor diff simple-todos-react.jsx
diff --git a/simple-todos-react/simple-todos-react.jsx b/simple-todos-react/simple-todos-react.jsx
index a7e2d2f..a67b030 100644
--- a/simple-todos-react/simple-todos-react.jsx
+++ b/simple-todos-react/simple-todos-react.jsx
@@ -1,3 +1,6 @@
+// Define a collection to hold our tasks
+Tasks = new Mongo.Collection("tasks");
+
 if (Meteor.isClient) {
   // This code is executed on the client only
```

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [!]
$ meteor diff App.jsx
diff --git a/simple-todos-react/App.jsx b/simple-todos-react/App.jsx
index 0d85460..6f6ab86 100644
--- a/simple-todos-react/App.jsx
+++ b/simple-todos-react/App.jsx
@@ -1,15 +1,19 @@
 // App component - represents the whole app
 App = React.createClass({
-  getTasks() {
-    return [
-      { _id: 1, text: "This is task 1" },
-      { _id: 2, text: "This is task 3" },
-      { _id: 3, text: "This is task 3" }
-    ];
+
+  // This mixin makes the getMeteorData method wor
+  mixins: [ReactMeteorData],
+
+  // Loads items from the Tasks collection and puts them on this.data.tasks
+  getMeteorData() {
+    return {
+      tasks: Tasks.find({}).fetch()
+    }
   },

   renderTasks() {
-    return this.getTasks().map((task) => {
+    // Get tasks from this.data.tasks
+    return this.data.tasks.map((task) => {
       return <Task key={task._id} task={task} />
     });
   },
```

4. Forms and events
-------------------

### Instructions

First, let's add a form to our `App` component:

#### 4.1  Add form for new tasks

##### `App.jsx`

```javascript
[...]
      <div className="container">
        <header>
          <h1>Todo List</h1>

          <form className="new-task" onSubmit={this.handleSubmit} >
            <input
              type="text"
              ref="textInput"
              placeholder="Type to add new tasks" />
          </form>
        </header>

        <ul>
[...]
```

Let's add a `handleSubmit` method to our `App` component:

#### 4.2  Add handleSubmit method to App component

##### `App.jsx`

```javascript
[...]
    });
  },

  handleSubmit(event) {
    event.preventDefault();

    // Find the text field via the React ref
    var text = React.findDOMNode(this.refs.textInput).value.trim();

    Tasks.insert({
      text: text,
      createdAt: new Date() // current time
    });

    // Clear form
    React.findDOMNode(this.refs.textInput).value = "";
  },

  render() {
    return (
      <div className="container">
[...]
```

#### Sorting our tasks

Currently, our code displays all new tasks at the bottom of the list. That's not very good for a task list, because we want to see the newest tasks first.

We can solve this by sorting the results using the `createdAt` field that is automatically added by our new code. Just add a sort option to the `find` call inside `getMeteorData` on the `App` component:

#### 4.3  Update getMeteorData to sort tasks by time

##### `App.jsx`

```javascript
[...]
  // Loads items from the Tasks collection and puts them on this.data.tasks
  getMeteorData() {
    return {
      tasks: Tasks.find({}, {sort: {createdAt: -1}}).fetch()
    }
  },
[...]
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [!]
$ git diff App.jsx
diff --git a/simple-todos-react/App.jsx b/simple-todos-react/App.jsx
index 6f6ab86..8e85145 100644
--- a/simple-todos-react/App.jsx
+++ b/simple-todos-react/App.jsx
@@ -7,7 +7,7 @@ App = React.createClass({
   // Loads items from the Tasks collection and puts them on this.data.tasks
   getMeteorData() {
     return {
-      tasks: Tasks.find({}).fetch()
+      tasks: Tasks.find({}, {sort: {createdAt: -1}}).fetch()
     }
   },

@@ -18,11 +18,33 @@ App = React.createClass({
     });
   },

+  handleSubmit(event) {
+    event.preventDefault();
+
+    // Find the text field via the React ref
+    var text = React.findDOMNode(this.refs.textInput).value.trim();
+
+    Tasks.insert({
+      text: text,
+      createdAt: new Date() // current time
+    });
+
+    // Clear form
+    React.findDOMNode(this.refs.textInput).value = "";
+  },
+
   render() {
     return (
       <div className="container">
         <header>
           <h1>Todo List</h1>
+
+          <form className="new-task" onSubmit={this.handleSubmit} >
+            <input
+              type="text"
+              ref="textInput"
+              placeholder="Type to add new tasks" />
+          </form>
         </header>

         <ul>
```

5. Update and remove
--------------------

### Instructions

Let's add two new elements to our `task` component, a checkbox and a delete button, with event handlers for both:

#### 5.1  Update Task component to add features

##### `Task.jsx`

```javascript
// Task component - represents a single todo item
Task = React.createClass({
  propTypes: {
    task: React.PropTypes.object.isRequired
  },

  toggleChecked() {
    // Set the checked property to the opposite of its current value
    Tasks.update(this.props.task._id, {
      $set: {checked: ! this.props.task.checked}
    });
  },

  deleteThisTask() {
    Tasks.remove(this.props.task._id);
  },

  render() {
    // Give tasks a different className when they are checked off,
    // so that we can style them nicely in CSS
    const taskClassName = this.props.task.checked ? "checked" : "";

    return (
      <li className={taskClassName}>
        <button className="delete" onClick={this.deleteThisTask}>
          &times;
        </button>

        <input
          type="checkbox"
          readOnly={true}
          checked={this.props.task.checked}
          onClick={this.toggleChecked} />

        <span className="text">{this.props.task.text}</span>
      </li>
    );
  }
});
```

### In my terminal emulator

```sh
Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [!]
$ git diff Task.jsx
diff --git a/simple-todos-react/Task.jsx b/simple-todos-react/Task.jsx
index c49e7ac..da01338 100644
--- a/simple-todos-react/Task.jsx
+++ b/simple-todos-react/Task.jsx
@@ -5,9 +5,37 @@ Task = React.createClass({
     // We can use propTypes to indicate it is required
     task: React.PropTypes.object.isRequired
   },
+
+  toggleChecked() {
+    // Set the checked property to the opposite of its current value
+    Tasks.update(this.props.task._id, {
+      $set: {checked: ! this.props.task.checked}
+    });
+  },
+
+  deleteThisTask() {
+    Tasks.remove(this.props.task._id);
+  },
+
   render() {
+    // Give tasks a different className when they are check off,
+    // so that we can style them nicely in CSS
+    const taskClassName = this.props.task.checked ? "checked" : "";
+
     return (
-      <li>{this.props.task.text}</li>
+      <li className={taskClassName}>
+        <button className="delete" onClick={this.deleteThisTask}>
+          &times;
+        </button>
+
+        <input
+          type="checkbox"
+          readOnly={true}
+          checked={this.props.task.checked}
+          onClick={this.toggleChecked} />
+
+        <span className="text">{this.props.task.text}</span>
+      </li>
     );
   }
 });
```

Shoichi at sho-mbp in ~/meteor-tutorials/simple-todos-react on master [!]
$

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

