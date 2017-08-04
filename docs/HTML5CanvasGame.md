#Creating Pong with HTML5 Canvas by Gunner Spencer

Hola! In this course we will take a look at creating games with HTML5 canvas and Javascript. We go over the basics of rendering a view, updating the game state, and receiving user input. It applies most of the skills covered in the <b>Beginner's Guide to Javascript</b>, so if I recommend you check that out if you don't have much experience with Javascript. Let's get started!

#### Project Setup
You will need a text editor (I recommend Atom.io or Textwrangler), but even Notepad will do. Setup a folder that will contain all of the files for this project, and name it something like JavascriptGuide (or don't, name it dankmemes if you want). And thats it! Open up your text editor and if you are using a more advanced text editor you can open up the path for your project folder and advance to the next step (don't worry if you can't, you will probably just need to leave the folder open in your system's file tree, i.e. Finder for Mac, so you can quickly access files inside of it.)

### Part 1: Setting the Stage

There is going to be very minimal HTML in this project, so let's just get that out of the way first:

index.html

	<!DOCTYPE html>
	<html>
		<head>
			<title>Lights, Camera, PONG!</title>
			<style>
				html, body {
					margin: 0px;
					padding: 0px;
					overflow: hidden;
				}
			</style>
		</head>
		<body>
			<script src="main.js"></script>
		</body>
	</html>
	
This is just setting up a simple HTML page. The only items of interest are the `style` tag, which is using a bit of CSS to make sure our screen doesn't have any unneeded white space, and the `script` tag which is just linking in our `main.js` file which we will create next:

main.js

	var canvas = document.createElement("canvas"),
		width = canvas.width = window.innerWidth,
		height = canvas.height = window.innerHeight;
		
	document.body.appendChild(canvas);
	
	var ctx = canvas.getContext("2d");
	
	ctx.fillRect(0, 0, width, height);
	
The first line of code should be familiar (if not, checkout Part 5 of the Beginner's Guide to Javascript). This just creates our DOM element of type `canvas`. Then we are creating two variables, `width` and `height`. We are setting those variables to the `canvas.width` and `canvas.height` respectively, which are in turn being assigned the value of `window.innerWidth` and `window.innerHeight` respectively. This ensures that our `canvas` takes up the entire size of our browser screen, and then we store those values in easier-to-use variables like `width` and `height`. If you wanted your game screen to be half the width and half the height of the screen, you would simply divide `window.innerWidth` or `window.innerHeight` divided by two in the assignment operation.

The next thing we do is put our canvas onto the body of our HTML page. Again, should be familiar code. Then we go into the most important variable for using HTML5 canvas, the `context` variable, or in this case we call it `ctx`. This is what we use to render onto our canvas. So, by storing the value of `canvas.getContext("2d")` into a variable, we can draw onto the canvas in two dimensions. 

That's where the next line comes in: `ctx.fillRect(x, y, width, height)`. This takes in four parameters and draws a rectangle at that location, with that width and height, in the current `ctx.fillStyle`, which by default is black. So by saving this and refreshing our index.html page in the browser, we should have a black screen. Perfect! 

### Part 2: A Paddle for the Battle

We are going to take a look at objects in Javascript, which essentially act as encapsulations for variables and functions that are associated with a certain aspect of our program. This is going to be a simplified version of Javascript objects, so if you want a more in-depth look check out the <b> OOPs, I Instantiated Again </b> lesson on SDCoding.

Let's get started:

	var paddle = {
		_x: 0,
		_y: 0,
		_width: 0,
		_height: 0,
		
		create: function(x, y, width, height) {
			var p = Object.create(this);
				p._x = x;
				p._y = y;
				p._width = width;
				p._height = height;
			return p;
		},
		
		render: function(c) {
			c.fillRect(this._x, this._y, this._width, this._height);
		},
		
		setX: function(x) {
			this._x = x
		},
		
		setY: function(y) {
			this._y = y;
		},
		
		getX: function() {
			return this._x;
		},
		
		getY: function() {
			return this._y;
		},
		
		getWidth: function() {
			return this._width;
		},
		
		getHeight: function() {
			return this._height;
		}
	};
	
This is our paddle object. We gave it some simple properties, like `_x` and `_height`, which by convention have the underscore before them. This isn't necessary though. Next we have our `create` function that takes in four parameters to use as properties. Here we are using the `Object.create` method of instantiating new objects in Javascript. After setting all of the properties, we return our new object. The four encapsulation functions, i.e., `getX`, `getY`, `setX`, `setY`, are there to facilitate the manipulation of our object's properties. The `render` function is simply there to draw a rectangle with the object's properties, with the parameter being of type `context` so that we can draw to it. Let's create our two paddles now:

	var playerPaddle = paddle.create(0, 0, 10, 100);
	var enemyPaddle = paddle.create(width - 10, 0, 10, 100);
	
Then let's create our `update` function to start rendering onto the screen. 

	function update() {
		ctx.fillStyle = "black";
		ctx.fillRect(0, 0, width, height);
		
		playerPaddle.render(ctx);
		enemyPaddle.render(ctx);
		requestAnimationFrame(update);
	}
	
And then make sure we call the `update` function. Our complete `main.js` file should look as follows:

	var canvas = document.createElement("canvas"),
		width = canvas.width = window.innerWidth,
		height = canvas.height = window.innerHeight;
		
	document.body.appendChild(canvas);
	
	var ctx = canvas.getContext("2d");
	
	ctx.fillRect(0, 0, width, height);
	
		var paddle = {
		_x: 0,
		_y: 0,
		_width: 0,
		_height: 0,
		
		create: function(x, y, width, height) {
			var p = Object.create(this);
				p._x = x;
				p._y = y;
				p._width = width;
				p._height = height;
			return p;
		},
		
		render: function(c) {
			c.fillRect(this._x, this._y, this._width, this._height);
		},
		
		setX: function(x) {
			this._x = x
		},
		
		setY: function(y) {
			this._y = y;
		},
		
		getX: function() {
			return this._x;
		},
		
		getY: function() {
			return this._y;
		},
		
		getWidth: function() {
			return this._width;
		},
		
		getHeight: function() {
			return this._height;
		}
	};
	
	var playerPaddle = paddle.create(0, 0, 10, 100);
	var enemyPaddle = paddle.create(width - 10, 0, 10, 100);
	
	update();
	
	function update() {
		ctx.fillStyle = "black";
		ctx.fillRect(0, 0, width, height);
		
		ctx.fillStyle = "white"; // change fill style to distinguish between the paddles and the background
		playerPaddle.render(ctx);
		enemyPaddle.render(ctx);
		requestAnimationFrame(update);
	}
	
### Part 3: Mouse Becomes One With Paddle

We are going to dive into user input now, so that we can adjust the position of our paddle, and then also implement some very rudementary AI to get the enemy paddle moving. Let's start by adding our event listener:

	document.body.addEventListener("mousemove", mouseMoveHandler);
	
	function mouseMoveHandler(event) {
		playerPaddle.setY(event.clientY - playerPaddle.getHeight() / 2);
	}
	
This will readjust our paddle to wherever our mouse is, centering the paddle on our mouse.

Now let's add the basic AI for our `enemyPaddle`:

In our `update` function, before we render the paddles, let's add a few conditional statements:
	
	var enemyPos = enemyPaddle.getY();
	
	// if the paddle is at the top of the screen, start moving down
	if(enemyPos < 0) {
		enemyVelocity *= -1;
	}
	
	// if the paddle is at the bottom of the screen, start moving up
	if(enemyPos + enemyPaddle.getHeight() > height) {
		enemyVelocity *= -1;
	}
  
    	// update the position of the enemy paddle
	enemyPaddle.setY(enemyPos + enemyVelocity);
	
These will make sure the `enemyPaddle` will stay on screen, and will move between the two boundaries. We need to create the `enemyVelocity` variable though. Near the top of our `main.js` file let's add this variable:

	var enemyVelocity = 5;
	
We can adjust the value of this to make it go faster or slower (the bigger we make it, the faster it goes).

### Part 4: Let's Get the Ball Rolling

Now it's time to create the `ball` object. This one will be relatively simple, since we don't need to make multiple copies of it:

	var ball = {
		_x: width / 2, // center the ball 
		_y: height / 2, // center the ball
		_vx: -4,
		_vy: 4,
		_size: 6,
		
		update: function() {
			this._x += this._vx;
			this._y += this._vy;
		},
		
		render: function(c) {
			c.beginPath();
			c.arc(this._x, this._y, this._size, 0, Math.PI * 2);
			c.fill();
			c.closePath();
		}
	};
	
The `update` function is here to make changing the position of our ball a little simpler, but it is not necessary. The `render` function is utilizing the `context.arc(x, y, radius, startAngle, endAngle)` function to draw a circle, and then fill it. Our `_vx` and `_vy` properties stand for the velocity of their respective dimensions. This controls how fast the ball is going and where it is going. If we add the following to our `update` function:

	ball.update();
	
and then render it 

	ball.render(ctx);
	
we should see a white ball moving from the center to the bottom left of our screen.

### Part 5: Pong, I Think We Need to Set Some Boundaries

We are almost there! Now the next step is to make the ball change directions when we hit it with our paddle, and also check if we or the enemy has missed it. This will all take place in the `update` function.

  	if(ball._y - ball._size < 0 || ball._y + ball._size > height) {
		ball._vy *= -1;
	}
	
	if(ball._x - ball._size < 0) {
		if(ball._y >= playerPaddle.getY() && ball._y <= playerPaddle.getY() + playerPaddle.getHeight()) {
			ball._vx *= -1;
		} else {
			enemyScore++;
			reset();
		}
	}
	
	if(ball._x + ball._size > width) {
		if(ball._y >= enemyPaddle.getY() && ball._y <= enemyrPaddle.getY() + enemyPaddle.getHeight()) {
			ball._vx *= -1;
		} else {
			playerScore++;
			reset();
		}
	}
	
These conditional statement are what's called edge handling, and just check everytime the screen re-renders if the ball is going to leave it. If it is, then we change the velocity if its going vertically off the screen, or we check if the paddle hit it if its horizontally moving off the screen.

### There is No Fairness in Love and War, Only in Keeping Score

Almost done! Now let's just add a way for us to see the scores. First, we need to create those variables, `playerScore` and `enemyScore`. Near where we created the `enemyVelocity` variable, let's create these:

	var enemyScore = 0,
		playerScore = 0;
		
Then, in our `update` function, lets add some code to render these scores:

	ctx.fillText(playerScore, width / 4, height / 10);
	ctx.fillText(enemyScore, width / 4 * 3, height / 10);
	
Now, let's create that `reset` function so that our `ball` will go back to the middle of the screen after a point has been scored.

	function reset() {
		ball._x = width / 2;
		ball._y = height / 2;
		ball._vx *= -1;
	}

#### Great Job!

You have succesfully created your very own HTML5 Canvas game. If you want to improve on this game, here are some of my suggestions: Make the AI better (like it tries to follow the ball's movements), adjust the velocity of the ball every time it resets (so that it hits at different angles), and then also try to make the game always work in proportion to whatever screen it is being played on.

The final `main.js` file should look as follows:

	var canvas = document.createElement("canvas"),
		width = canvas.width = window.innerWidth,
		height = canvas.height = window.innerHeight;
    
 	var enemyVelocity = 5;
  	var enemyScore = 0,
		playerScore = 0;
		
	document.body.appendChild(canvas);
	
	var ctx = canvas.getContext("2d");
	
	ctx.fillRect(0, 0, width, height);
	
		var paddle = {
		_x: 0,
		_y: 0,
		_width: 0,
		_height: 0,
		create: function(x, y, width, height) {
			var p = Object.create(this);
				p._x = x;
				p._y = y;
				p._width = width;
				p._height = height;
			return p;
		},
		
		render: function(c) {
			c.fillRect(this._x, this._y, this._width, this._height);
		},
		
		setX: function(x) {
			this._x = x
		},
		
		setY: function(y) {
			this._y = y;
		},
		
		getX: function() {
			return this._x;
		},
		
		getY: function() {
			return this._y;
		},
    
    		getWidth: function() {
			return this._width;
		},
		
		getHeight: function() {
			return this._height;
		}
	};
  
  	var ball = {
		_x: width / 2, // center the ball 
		_y: height / 2, // center the ball
		_vx: -4,
		_vy: 4,
		_size: 6,
		
		update: function() {
			this._x += this._vx;
			this._y += this._vy;
		},
		
		render: function(c) {
			c.beginPath();
			c.arc(this._x, this._y, this._size, 0, Math.PI * 2);
			c.fill();
			c.closePath();
		}
	};
	
	var playerPaddle = paddle.create(0, 0, 10, 100);
	var enemyPaddle = paddle.create(width - 10, 0, 10, 100);
  
  	document.body.addEventListener("mousemove", mouseMoveHandler);
	
	function mouseMoveHandler(event) {
		playerPaddle.setY(event.clientY - playerPaddle.getHeight() / 2);
	}
  
  	function reset() {
		ball._x = width / 2;
		ball._y = height / 2;
    ball._vx *= -1;
	}
	
	update();
	
	function update() {

		ctx.fillStyle = "black";
		ctx.fillRect(0, 0, width, height);
    
      	if(ball._y - ball._size < 0 || ball._y + ball._size > height) {
		ball._vy *= -1;
	}
	
	if(ball._x - ball._size < 0) {
		if(ball._y >= playerPaddle.getY() && ball._y <= playerPaddle.getY() + playerPaddle.getHeight()) {
			ball._vx *= -1;
		} else {
     	enemyScore++;
      reset();
		}
	}
	
	if(ball._x + ball._size > width) {
		if(ball._y >= enemyPaddle.getY() && ball._y <= enemyPaddle.getY() + enemyPaddle.getHeight()) {
			ball._vx *= -1;
		} else {
  	playerScore++;
    reset();
		}
	}
		
    	var enemyPos = enemyPaddle.getY();
	
	
	// if the paddle is at the top of the screen, start moving down
	if(enemyPos < 0) {
		enemyVelocity *= -1;
	}
	
	// if the paddle is at the bottom of the screen, start moving up
	if(enemyPos + enemyPaddle.getHeight() > height) {
		enemyVelocity *= -1;
	}
  
    	// update the position of the enemy paddle
	enemyPaddle.setY(enemyPos + enemyVelocity);
    
    ball.update();
    ctx.fillStyle = "white";
		playerPaddle.render(ctx);
		enemyPaddle.render(ctx);
    ball.render(ctx);
    
    	ctx.fillText(playerScore, width / 4, height / 10);
	ctx.fillText(enemyScore, width / 4 * 3, height / 10);
		requestAnimationFrame(update);
	}
	
Checkout the final result at <a href="https://jsfiddle.net/jshsdgkk/42/">https://jsfiddle.net/jshsdgkk/42/</a>!