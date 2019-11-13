# LeafMVC

Leaf MVC is a simple PHP framework that allows you to create powerful web apps and APIs quickly and efficiently. Leaf MVC is powered by the [Leaf Core](https://leaf-docs.netlify.com) and is based on the Ruby on Rails and Laravel frameworks.

# Getting Started
## Installation
With LeafMVC, you can whip up a full MVC app in a couple of seconds. Leaf MVC's recommended mode of installation is with [composer](https://getcomposer.org).
```bash
composer create-project leafs/mvc <project-name>
```
This will create a LeafMVC project and install all dependencies. Also, a `.env` file will be created for you.
You can serve your project with 
```bash
php leaf serve
```

## Folder Structure
```bash
C:.
├───app
│   ├───controllers
│   ├───helpers
│   ├───migrations
│   ├───models
│   ├───routes
│   └───views
│       └───dist
├───config
│   └───command
│       └───stubs
├───lib
├───public
├───storage
└───vendor
```
As you can see, the structure of Leaf MVC isn't so different from other frameworks like Rails and Laravel, let's take a deeper look at the folder structure 

`app` is where the main code for the app sits. All the controllers, models, views, helpers, migrations and routes. 

`config` holds configuration files for the Leaf framework, ie, Command Line suuport and class autoloader 

`lib` is where additional library support would be kept if need be 

`public` holds compiled assets which web browsers can use 

`storage` is meant to hold "uploaded" files 

`vendor` is where all Leaf MVC's dependencies are kept.


## Basic Usage
LeafMVC is created with Leaf Core, hence, you can still use the Leaf Code you're used to.<br>
`app/routes/routes.php`
```javascript
<?php
$leaf->get('/home', function() use($response) {
  $response->respond(['Message' => 'Hello World']);
});
```
Just enter this code and run `php leaf serve` and navigate to localhost:3000
It's that simple to build with LeafMVC

<br>
<br>

# <a href="#/first-app/">Building your first leaf app</a>
# <a href="#/cmd/">Leaf CMD</a>
# <a href="#/routing/">Routing</a>
# <a href="#/controllers/">Controllers</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>