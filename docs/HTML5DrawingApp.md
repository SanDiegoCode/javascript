# Drawing App with HTML5 Canvas and Javascript

Prerequisites: a brain and some basic knowledge of HTML and Javascript.

[End Product](https://codepen.io/ronakshah/full/rzOgaQ/): a semi-functional, semi-user-friendly, super-cool web app that allows you to draw with your mouse and change the color/size/type of drawing tool.

#### Project Setup
You will need a text editor (I recommend [Atom.io](https://atom.io/) or [Textwrangler](https://www.barebones.com/products/textwrangler/)), but even Notepad will do. Setup a folder that will contain all of the files for this project, and name it something like `JavascriptDrawingApp` (or don't, name it dankmemes if you want). And thats it! Open up your text editor and if you are using a more advanced text editor you can open up the path for your project foldner and advance to the next step (don't worry if you can't, you will probably just need to leave the folder open in your system's file tree, i.e. Finder for Mac, so you can quickly access files inside of it.)

If you're on the web, you can use [Codepen Projects](https://codepen.io/project)

### Step 1
Create your `index.html` file and add the following: 

	<!DOCTYPE html> 
	<html>
		<head>
			<title> My cool drawing app </title>
			<style>
				html, body {
					margin: 0px;
					padding: 0px;
					overflow-x: hidden;
				}
			</style>
		</head>
		<body>
			<canvas id="paper"></canvas>
			<script src="main.js"></canvas>
		</body>
	</html>

This is just setting up a basic HTML file that has the small amount of CSS we need in a `<style>` tag. All the CSS is doing is making sure that our canvas will be able to take up the entire browser screen by eliminating any extra space. Then in our `<body>` we have our `<canvas id="paper"></canvas>` that we will use in our Javascript to draw to, and then our `<script>` tag requesting the Javascript resource, `main.js` that we will create next.

### Step 2
In the same folder as your `index.html` file, create a `main.js` file and enter the following:

	var canvas = document.getElementById("paper"),
		ctx = canvas.getContext("2d"),
		width = canvas.width = window.innerWidth,
		height = canvas.height = window.innerHeight;
		

This Javascript code is initializing a couple of variables, the first being `canvas`, which is initialized to a DOM (Document Object Model) function `document.getElementById(id)` that returns the HTML element with the corresponding id in our index.html file (in this case, our `<canvas id="paper"></canvas>` element. After this assignment we move onto our context variable, `ctx`, which calls the function `getContext("2d")` on our recently created `canvas` variable in order to return an object that we can use to draw onto our `canvas` with. Finally, the variables `width` and `height` are initiated and in a chain of assignment operatiosn are first set to the corresponding `canvas` property, which in turn is assigned the value of `window.innerWidth` or `window.innerHeight` which is a Javascript engine model property that returns the full width and height of our browser screen in pixels, respectively. (NOTE: although the values of `window.innerWidth` and `window.innerHeight` are representative of pixels, their actual values are just numbers, i.e, `600` or `920.60`).

### Step 3
Now it is time to add some event listeners! What are those? Well, the browser is waiting for you to interact with the computer (like its listening for something), and then when you do something, like press a key or move your mouse, it triggers what is called an `event` which allows us as programmers to use that event data. We can add different kinds of `listeners` to our HTML elements that perform different functions when different events are "fired" (which just means they happend, like a click).

In our `main.js` file lets add some event listeners: 

	canvas.addEventListener("mousedown", mouseDownEvent);
	canvas.addEventListener("mousemove", mouseMoveEvent);
	canvas.addEventListener("mouseup", mouseUpEvent);
	
Each of these functions is adding a different type of listener to the `canvas`. Each function takes in two parameters (those are the things within the parentheses separated by commas). The first parameter is in quotes, because it is a string value, and tells the function what type of listener to add to our `canvas` object. The second parameter is a function that we want to be called (or executed) whenever that event fires. We will create these functions next.

Right now our `index.html` file should look the same as in <b> Step 1</b>, and our `main.js` should look as follows:

	var canvas = document.getElementById("paper"),
	ctx = canvas.getContext("2d"),
	width = canvas.width = window.innerWidth,
	height = canvas.height = window.innerHeight;
		
	canvas.addEventListener("mousedown", mouseDownEvent);
	canvas.addEventListener("mousemove", mouseMoveEvent);
	canvas.addEventListener("mouseup", mouseUpEvent);	
### Step 4
Now let's create those functions, known as <b>Event Handlers</b>. 

Add the following to your `main.js` file:

	function mouseDownEvent(event) {
		drawAt(event.clientX, event.clientY);
		drawing = true;
	}
	
	function mouseMoveEvent(event) {
		if(drawing) {
			drawAt(event.clientX, event.clientY);
		}
	}
	
	function mouseUpEvent() {
		drawing = false;
	}
	
The first function, `mouseDownEvent(event)` is taking in the `event` object as a parameter, and using its `clientX` and `clientY` properties in the `drawAt` function, which we will create in a moment. It also sets the variable `drawing` to true, something else that will be added in a moment.

The second function, `mouseMoveEvent(event)` is again taking in the `event` parameter that is passed in by the event listener to check if we are drawing (a.k.a. if the mouse is being pressed), and if so then use the `drawAt` function to draw at the `clientX` and `clientY` location.

The third function, `mouseUpEvent()` is going to simply set `drawing` to false, so that way we aren't adding anything onto our `canvas` when the mouse isn't being pressed.

### Step 5
Create the `drawAt` function and a few other variables.

In our `main.js` file lets add the `drawing` variable.

At the top of our file, below our variables initializations, create a new variable:

	var drawing = false;

This is going to help us check if we have the mouse pressed or not, and thus whether we should be drawing.

Add these other variables too:

	var color = "black";
	var size = 10;
	var type = "square";
	
Now we are going to make use of these new variables in our `drawAt` function.

Let's create that now, adding it below those variables we just made:

	function drawAt(x, y) {
		ctx.fillStyle = color;
		if(type.toLowerCase().trim() == "square") {
			var kx = x - size / 2,
				ky = y - size / 2;
			ctx.fillRect(kx, ky, size, size);
		} else if(type.toLowerCase().trim() == "circle") {
			ctx.beginPath();
			ctx.arc(x, y, size, 0, Math.PI * 2);
			ctx.fill();
			ctx.closePath();
		}
	}
	
Wow! Okay thats a hefty function, so let's dissect it a bit. 

After declaring the function (saying function and then the function name, `drawAt`) with our `x` and `y` parameters, the first thing to notice is we assign `ctx.fillStyle` to our `color` variable. This assures that whenever we draw it will always be in whatever value is stored in the `color` variable. 

The next thing is component is an if, else if block that checks if our `type` is a square or a circle. It converts our `type` function to `toLowerCase` and then uses `trim` to get rid of excess white space. This ensures that the values are not case-sensitive.

If we move into our `square` part of the if, else if block, we will see some code that initializes two variables: `kx` and `ky`. These are simply computing the coordinates of the midpoint of the square we want to draw by subtracting half of the `size` variable from each value. Then, using the `fillRect` function on our `ctx` variable, we can draw a rectangle at that location at the specified (x, y, width, height). Our `size` variable takes care of the `width` and `height` of our square, while our newly calculated midpoint coordinates take the place of `x` and `y`.

Moving into our `circle` part of the if, else if block we will see code for creating a circle in canvas. The first step is using `beginPath` then using `arc(x, y, radius, startAngle, endAngle)` to draw a circle. Here we use the raw `x` and `y` with our `size` variable as the radius, and then `0` as our startAngle and `Math.PI * 2` as the endAngle in order to get a full circle. After this, we `fill` it and then `closePath`.

Great job! Our drawing app is nearly completed. Your `main.js` file should look like the following: 

	var canvas = document.getElementById("paper"),
	ctx = canvas.getContext("2d"),
	width = canvas.width = window.innerWidth,
	height = canvas.height = window.innerHeight;
	
	var drawing = false;
	var color = "black";
	var size = 10;
	var type = "square";
	
	function drawAt(x, y) {
		ctx.fillStyle = color;
		if(type.toLowerCase().trim() == "square") {
			var kx = x - size / 2,
				ky = y - size / 2;
			ctx.fillRect(kx, ky, size, size);
		} else if(type.toLowerCase().trim() == "circle") {
			ctx.beginPath();
			ctx.arc(x, y, size, 0, Math.PI * 2);
			ctx.fill();
			ctx.closePath();
		}
	}
		
	canvas.addEventListener("mousedown", mouseDownEvent);
	canvas.addEventListener("mousemove", mouseMoveEvent);
	canvas.addEventListener("mouseup", mouseUpEvent);
	
	function mouseDownEvent(event) {
		drawAt(event.clientX, event.clientY);
		drawing = true;
	}
	
	function mouseMoveEvent(event) {
		if(drawing) {
			drawAt(event.clientX, event.clientY);
		}
	}
	
	function mouseUpEvent() {
		drawing = false;
	}
	
At this point, you can start drawing on your browser by opening up the `index.html` file in Google Chrome for example. However, there are a few more things we need to add in order to customize our drawing tool while we draw and save our drawings.

### Step 6
Now we will add another listener, in order to receive keyboard input and change the values of our variables real-time.

Add the following event listener with the others you have already created in your `main.js`.

	document.body.addEventListener("keydown", keyDownEvent);
	
Notice that we are using `document.body` and not `canvas` this time.

Now, let's create this event handler:

	function keyDownEvent(event) {
		switch(event.keyCode) {
			case 67: // c
				color = prompt("What color do you want to draw with?");
				break;
			case 83: // s 
				size = parseInt(prompt("What size do you want to draw with?"));
				break;
			case 84: // t 
				type = prompt("What type of tip do you want to draw with? (square or circle)");
				break;
		}
	}
	
The `keyDownEvent(event)` function is going to use a `switch` statement to check the value of `event.keyCode` in order to see if any of the keys we care about were pressed. The `switch` statement is going to go through case by case, entering the case block if the value in `switch(value)` is equal to the value of the case. Once it reaches the end of the statement or a `break` it jumps out of the function. 

We are checking if the keys `c`, `s`, and `t`, are pressed. When `c` is pressed we prompt the user for a new color. When `s` is pressed we prompt the user for a new size, and then use the `parseInt` function to retrieve an integer value from the string that is returned by `prompt`. Then if `t` is pressed we prompt the user for a new type. For all of these prompts we assign the return values to their respective variables.
if we add in this function by our other event handlers and run the code, we should be able to change the color, size, and type of drawing tool we use by pressing the `c`, `s`, and `t`, keys, respectively.

Home stretch! We have one final step to top off this lesson.

### Step 7
Now we will be creating the functionality to save our beautiful drawings.

In our `keyDownEvent` function, go into the `switch` statement and after the last `break` add another `case` like so:

	case 32: // space bar
		var imageData = canvas.toDataURL(),
			name = "Image" + Date.now();
		var download = document.createElement("a");
			download.setAttribute("href", imageData);
			download.setAttribute("download", name);
			download.innerHTML = name;
			
		var br = document.createElement("br");
			
		document.body.appendChild(br);
		document.body.appendChild(download);
		break;

This `case` will trigger when the spacebar is pressed, creating an `<a></a>` tag with Javascript using the `document.createElement(name)` method, then setting it's `href` attribute to the `imageData` which we retrieve with the `canvas.toDataURL` function. This, in conjunction with the `download` attribute, will allow us to download the current image on our canvas. Next we set the `innerHTML` so that a name displays, this name being a concatenation of "Image" and the current time in milliseconds using `Date.now()`. Next, we create a `<br/>` element to space out our download links as they are created, then append these to our `document.body`, remembering to add the `break` at the end. 


**Great job!**

You have succesfully created a drawing app where you can customize your brush and download your masterpieces. Be sure to share this with all of your friends!

The final status of `main.js` is shown below:

	var canvas = document.getElementById("paper"),
	ctx = canvas.getContext("2d"),
	width = canvas.width = window.innerWidth,
	height = canvas.height = window.innerHeight;
	
	var drawing = false;
	var color = "black";
	var size = 10;
	var type = "square";
	
	function drawAt(x, y) {
		ctx.fillStyle = color;
		if(type.toLowerCase().trim() == "square") {
			var kx = x - size / 2,
				ky = y - size / 2;
			ctx.fillRect(kx, ky, size, size);
		} else if(type.toLowerCase().trim() == "circle") {
			ctx.beginPath();
			ctx.arc(x, y, size, 0, Math.PI * 2);
			ctx.fill();
			ctx.closePath();
		}
	}
		
	canvas.addEventListener("mousedown", mouseDownEvent);
	canvas.addEventListener("mousemove", mouseMoveEvent);
	canvas.addEventListener("mouseup", mouseUpEvent);
	document.body.addEventListener("keydown", keyDownEvent);
	
	function mouseDownEvent(event) {
		drawAt(event.clientX, event.clientY);
		drawing = true;
	}
	
	function mouseMoveEvent(event) {
		if(drawing) {
			drawAt(event.clientX, event.clientY);
		}
	}
	
	function mouseUpEvent() {
		drawing = false;
	}
	
	function keyDownEvent(event) {
		switch(event.keyCode) {
			case 67: // c
				color = prompt("What color do you want to draw with?");
				break;
			case 83: // s 
				size = parseInt(prompt("What size do you want to draw with?"));
				break;
			case 84: // t 
				type = prompt("What type of tip do you want to draw with? (square or circle)");
				break;
			case 32: // space bar
				var imageData = canvas.toDataURL(),
				name = "Image" + Date.now();
				var download = document.createElement("a");
					download.setAttribute("href", imageData);
					download.setAttribute("download", name);
					download.innerHTML = name;
			
				var br = document.createElement("br");
			
				document.body.appendChild(br);
				document.body.appendChild(download);
				break;
		}
	}
