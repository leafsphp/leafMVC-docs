# Working with controllers
If you read [creating your first LeafMVC app](/first-app/), you should already have an idea on how to work with `controllers`, but in this section, we'll be going into details.


So basically, we'll be looking at both Web and API controllers, creating controllers and controller methods provided by Leaf Core.


# Generating Controllers
With LeafMVC, all controllers are kept in the `app/controllers` directory. So you can manually create your own Controller there, but the recommended method is to use the leaf CMD tool. So, in the root of your leaf MVC project, openup your console and type:
```bash
php leaf g:controller <Name>
```

# A deep look at controllers
As mentioned before, LeafMVC has 2 types of controllers: API controllers and web controllers. Though they're both controllers,  they offer different base methods for different purposes. For instance, The web controllers come pre-packaged with Leaf Veins.


## Web Controllers
First, let's look at Web Controllers.
```javascript
<?php
    namespace App\Controllers;

    use Leaf\Core\Controller;

    class ClassName extends Controller {
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
This is the default boilerplate generated for the web controller. As mentioned before, LeafMVC uses Leaf Core's controller packages which we extend to create our own controller. This provides us with Leaf Core's helper methods and Leaf Vein integration. Vein is Leaf's  default templating engine. You can read more on veins [here](/veins/).


To use this model to resolve a route, you simply have to pass it into the route like this:
```javascript
$leaf->get('/home', '\App\Controllers\ClassName@index');
```


## API Controllers
```javascript
<?php
    namespace App\Controllers;

    use Leaf\Core\ApiController;

    class ClassName extends ApiController {
        public function __construct() {
            parent::__construct();
        }

        public function index() {
            $this->respond([
				"message" => "This is the ClassName"
			]);
        }

        public function create() {
            
        }

        public function show() {

        }

        public function destroy() {

        }
    }
```
This is the default boilerplate generated for the API controller. The API controller has a bunch of handy methods that can be used to handle responses to the user. Some of these are:


`respond()` this takes in an array and displays the data to the user in JSON format


`respondWithCode()` this takes in an array and an HTTP code(integer). It displays the data to the user in JSON format with the HTTP code.


<br>
<br>

# <a href="#/veins/">Veins</a>
# <a href="#/cmd/">Leaf CMD</a>
# <a href="#/routing/">Routing</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>