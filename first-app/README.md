# Building your first LeafMVC app
Note that all your development is done in the `app` directory. By default, a few demos have been created to give you a quick idea on how LeafMVC works.


# Introduction
For this "tutorial", we'll be building a simple project to learn about Leaf in general. We're going to be simulating all the data in the model, i.e, we're not going to use a database in this "tutorial".

In the [previous section](/?id=leafmvc), we looked at installation, LeafMVC's directory structure and a basic usage example, it's assumed you've already read this section.

Also, we'll be using Leaf's console to generate our files, so, it's recommended that you check out [this section](/cmd/)

Now that that's out of the way, we can start with our actual development. When we take a look at our `index.php` file, we see that Leaf Core is initialise with a couple of it's functions(`$request` and `$response`)

We're also importing our routes from `app/routes/routes.php`
```javascript
<?php
require_once __DIR__ . '/vendor/autoload.php';

require __DIR__. "/config/bootstrap.php";

$leaf = new Leaf\Core\Leaf;
$response = new Leaf\Core\Http\Response;
$request = new Leaf\Core\Http\Request;
$errors = new Leaf\Config\Errors;

$errors->hide();

require __DIR__. "/app/routes/routes.php";

$leaf->run();
```
This is the index.php generated for you.

As mentioned before, all our development happens in our `app` directory, so, let's move into our app directory. As we saw in `index.php`, our routes were defined in the `app/routes` directory. This will be a good starting point. Open up your `routes.php`

(NB: Routing is a feature of Leaf Core)
To use simple routing with leaf, you simply need to define individual routes to be handled by the Leaf Router. Lets look at that.
```javascript
<?php
$leaf->get('/', function() {
	// Do something here
});
```
So we can return json encoded data for APIs, html and php pages, raw text......

But in this case we're workinh in an MVC environment, we would want controllers to handle various routes, so, let's do just that.

Remember we talked about the Leaf Console? We're going to generate a controller now.
```bash
php leaf g:controller Pages
```
This will generate a controller in our `app/controllers` directory

Back in our `app/routes/routes.php` file, we can use this controller like so:
```javascript
$leaf->get('/home', '\App\Controllers\PagesController@index');
```
That's it. Now, let's look at our controller

```javascript
<?php
namespace App\Controllers;
use Leaf\Core\Controller;

class PagesController extends Controller {
	public function __construct() {
		parent::__construct();
	}
	public function index() {
		$this->set([
			"title" => "Leaf Vein Integration"
		]);
		$this->render("index");
	}
	public function create() {
		
	}
	public function show() {
	}
	public function destroy() {
	}
}
```
By default, LeafMVC's controllers are set-up to use Leaf's templating engine(Veins). Veins are very flexible and easy to use, making them a good choice for LeafMVC. You can quickly get this to work by running
```bash
php leaf g:template index
```

This will generate a new Vein, `index.vein` in `app/views`. Just reload your app to see the new vein. With this, we have set up a view and a controller. One major use of MVC(VC) is to be able to pass data to the view from the controller. Let's see how that works in LeafMVC.

Let's go back to our controller. Let's say we have a new variable(object) which contains user info
```javascript
$user = (object) [
	'name' => 'Jane Doe',
	'email' => 'janedoe@gmail.com',
	'logged' => true
];
```
and we want to pass this into our View, we can do this simply with by passing this variable through Leaf Core's already defined `set()`, let's see how that works.

```javascript
public function index() {
	$user = (object) [
		'name' => 'Jane Doe',
		'email' => 'janedoe@gmail.com',
		'verified' => true
	];
	$this->set($user);
	$this->render("index");
}
```
With this, we are passing the user object into our Vein Template. You can read more on Vein Templating [here](/templating/).

Now, open up `app/views/index.vein` you're to see this
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>{$title}</title>
	<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
</head>
<body>
	<h2>{$title}</h2>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>
</body>
</html>
```

To use a variable passed into Veins, we use `{$variable}`, since we passed in the user object, we can use it's components here: eg `{$name}`. Lets see how that works.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Index</title>
	<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
</head>
<body>
	<h2>{$name}</h2>
	<p>{$email}</p>
	{if="$verified"}
		<p>User is verified</p>
	{else}
		<p>User is not verified</p>
	{/if}
	<script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>
</body>
</html>
```
Now, we've looked at our View and our Controller. Let's talk about Models. Our models are kept in the `app/models` directory. Models usually handle data: workk with databases, data storage...Models pass required information into our controller, which is then passed into the view. Let's first generate a model.
```bash
php leaf g:model Test
```

This will generate a simple model
```javascript
<?php
    namespace App\Models;

    use Leaf\Core\Database;
    new Database();

    use Leaf\Core\Model;

    class Test extends Model {
        protected $fillable = [

        ];
    }
```

As mentioned before, we'll be faking all our data, we won't be using any database. So, in this case, the data we're going to be passing into our Controller is the user array we used earlier. 
```javascript
<?php
    namespace App\Models;

    use Leaf\Core\Database;
    new Database();

    use Leaf\Core\Model;

    class Test extends Model {
        public function getUser() {
			// we get user from some source and save it as a user object
			$user = (object) [
				'name' => 'Jane Doe',
				'email' => 'janedoe@gmail.com',
				'verified' => true
			];
			// we return the user object
			return $user;
		}
    }
```

To use this in our controller, we simply have to initialise the model in our controller. Let's edit the current controller we have now.
```javascript
<?php
namespace App\Controllers;
use Leaf\Core\Controller;

// use our model
use App\Models\Test;

class PagesController extends Controller {
	public function __construct() {
		parent::__construct();
		// initialise the model
		$this->test = new Test();
	}
	public function index() {
		// get the user object from Test model
		$user = $this->test->getUser();
		// pass user into our view
		$this->set($user);
		$this->render("index");
	}
	public function create() {
		
	}
	public function show() {
	}
	public function destroy() {
	}
}
```
Our View remains the same.

With this basic set-up, we have just built an MVC application, not so useful, but it's still an MVC app😅😅


<br>
<br>

# <a href="#/cmd/">Leaf CMD</a>
# <a href="#/routing/">Routing</a>
# <a href="#/controllers/">Controllers</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>