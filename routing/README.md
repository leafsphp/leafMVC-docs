# Routing
All Leaf MVC's routes are kept in `app/routes`. Leaf MVC uses Leaf Core's router for it's routing. This means that it's the same as Leaf's routing. You can check it out [here](https://leaf-docs.netlify.com/v1.4.2/routing/simple-routing.html)


# Sample Routes
```javascript
// get request
$leaf->get('/user/{id}', function($id) {
	$response->respond([
		"mesage" => "Your id is $id"
	]);
});

// using controllers
$leaf->get('/user/{id}', 'Class@method');
```

<br>
<br>

# <a href="#/cmd/">Leaf CMD</a>
# <a href="#/veins/">Veins</a>
# <a href="#/controllers/">Controllers</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>