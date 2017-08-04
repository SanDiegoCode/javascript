# A Beginner's Guide to Javascript by Gunner Spencer

Hello there! Welcome to this course that will teach you all of the basics of the Javascript programming language. Javascript allows us to program applications and webpages for the web browser (like Google Chrome or Internet Explorer). Think of it as the brains of the operation, that works on the client side (which means it doesn't talk to the server), in order to provide your webpage with functionality. Let's just jump right in to start getting a better understanding!

#### Project Setup
You will need a text editor (I recommend Atom.io or Textwrangler), but even Notepad will do. Setup a folder that will contain all of the files for this project, and name it something like JavascriptGuide (or don't, name it dankmemes if you want). And thats it! Open up your text editor and if you are using a more advanced text editor you can open up the path for your project folder and advance to the next step (don't worry if you can't, you will probably just need to leave the folder open in your system's file tree, i.e. Finder for Mac, so you can quickly access files inside of it.)

### Part 1: Two Worlds Collide, HTML & Javascript

The first thing we need to do before we even begin writing any Javascript is to create an `index.html` file. To do this, use your text editor to create a new file, then save that file as `index.html`.

 <b>NOTE: Whenever you make changes to any file, you have to save it before seeing those changes reflected in the browser.</b>

	<!DOCTYPE html>
	<html>	
		<head>
			<title> Javascript Tutorial </title>
		</head>
		<body>
			<script src="main.js"></script>
		</body>
	</html>
	
This just creates a basic HTML page that we can open up with the web browser of our choice (find the `index.html` file and right click it, then press open with and select the web browser). All we are doing on this webpage is giving it a title: `Javascript Tutorial` and then in our `body` tags, creating `script` tags to import our Javascript file by setting `src`, standing for source, to our `main.js` file, which we will create next.

### Part 2: O, Where art Thou, Variables
Now it's time for our `main.js` file! Create it in the same way you created the `index.html` file, except of course with our new name, `main.js`. Notice that a Javascript file will always have the extension `.js`. This lets the browser know what type of file it is.

Open up your `main.js` and type the following:

	var MyVariable = "Hello World!";
	
	console.log(MyVariable);

Now save this file and refresh your webpage. Nothing happened! Or so it seems. Right click the browser screen (if you are using Safari, switch to another browser, otherwise this won't work), and press Inspect Element, or Inspect. A box should pop up somewhere on your browser window that has the HTML code we wrote for our `index.html` file. Go to the top of that box and click where it says `Console`. Here you will see the output of our function we just called, `console.log`. 

To call a function is to make that piece of code inside the function run. We pass what are called `parameters` to functions, the things inside the parentheses of the function call. These are used by the function, like how `console.log(text)` takes in the parameter `text` to output to the console.

The parameter that we passed into the function was actually a variable, specifically, `MyVariable`, which had a value of `"Hello World!"`. Variables are found in all programming langauges, as they allow us to store data for later use in our program. There are different types of data, for example: numbers, strings (which are just words or letters, like the value of `MyVariable`), and booleans. By creating a variable, we can, instead of using the string `"Hello World!"`, just use the name of the variable, `MyVariable`, in its place. The same goes for numbers in mathematical operations (which we will see in a moment) or boolean values (true or false) in conditional statements. 

Below are examples of the different variables, including numbers, and the mathematical operations we can do with them.


	var count = 5; // just a number
	var num = 10.5; // a floating point number, or decimal
	var product = count * num; // multiplication operator
	var quotient = num / count; // division operator
	var added = count + num; // addition operator
	var subtracted = num - count; // subtraction operator
	
	product = quotient * added; 
	/* notice that we don't have to add the keyword var 
	after we already created the variable. */
	
	subtracted = product - subtracted; 
	/* we can use the variable we are assigning a value to 
	inside of the right-hand operation */
	
	var crazyOperation = ((count * 5) / (product + added)) * quotient / 1.5; 
	/* this demonstrates the order of operations, which is 
	the same as in your regular math class, but we use 
	parentheses for nested statements that we want to make 
	sure get evaluated first */
	
Try these out, using `console.log` to view the values you get. The `//` is a single line comment, so everything else after the `//` in that line is ignored. Same thing with the `/*   multiline comment   */` which can span multiple lines. Just make sure you open up with `/*` and then write your comment, then close it `*/`.

	var firstName = "Johnny";
	var lastName = "Appleseed";
	var fullName = firstName + " " + lastName;
	
	var nameSize = fullName.length;
	
These are examples of how you can use `strings`, the data type that allows you to store letters/characters in a variable. Note that `strings` have built-in attributes, like the `length` attribute that returns the length of that string. Also, we can combine, or concat, `string` with `+` signs. That's how we get the value for our `fullName` variable. Try using `console.log` to view the values!

	var continue = false;
	// some stuff we do before we continue
	continue = true;
	
This is a boolean variable. It holds the value of either `true` or `false`, which will allow us to evaluate conditional statements, a concept we will jump into next.

	
### Part 3: It's True, Javascript is the Language for You
This next concept is crucial to programming. It is the conditional statement, which essentially checks if a condition is true or false, then does something accordingly. In Javascript, we have a few of these:

	var count = 5,
		measure = 20;
	
	if(count < measure) {
		console.log("count is less than measure");
		if(count > measure / count) {
			console.log("we can put if statements inside of if statements, and also use mathematical operations in the condition brackets!");
		}
	} else {
		console.log("this code would run if the condition was not true.");
	}
	
This is the most fundamental conditional statement, the `if else` statement. It checks if the condition inside the parentheses is true, and if it is it executes the code inside of the curly brackets. Otherwise, it executes the code following the `else` keyword. There are a few conditional operators we can use to compare values: `==, >, <, >=, <=, !=`. These are pretty intuitive, meaning is equal to, greater than, less than, greater than or equal to, less than or equal to, and is not equal to, respectively. 

	var count = 0;
	while(count < 10) {
		console.log(count);
		count++; // same thing as count += 1, count = count + 1
	}

This is a `while` loop, which executes the code inside the curly braces while the condition in the parentheses is true. Test out this piece of code, even see if you can make it count by two's or three's. 

	for(var count = 0; count < 10; count++) {
		console.log(count);
	}
	
This is a `for` loop, which essentially combines the components of a `while` loop necessary for iteration into one concise statement. This does the exact same thing as the previous conditional loop, except the syntax is different, since the iterator (or variable we increment) is declared inside the `for` statement, along with the condition to check and the iteration command `count++`.

### Part 4: Putting the Fun in Functions
So far we have looked at Javascript code that executes in a linear fashion. This means that the Javascript engine, which runs our code, is starting from the top of our file and executes the code line by line until it reaches the end. Things like conditional statements and loops can skip over certain pieces of code, but for the most part, there is only linear progression. This is great, except for what if we wanted to do the same thing in two places in our code? Would we have to rewrite the same code? No! That's where functions come in. Functions act as blocks that contain code we can execute from anywhere in our program, again and again. We have already seen examples of this, like `console.log`, which receives a parameter, like the text we want to output, and uses it inside of the code contained in that function. Let's take a look at how a function works in code!

	function addTwoNumbers(num1, num2) {
		var result = num1 + num2;
		return result;
	}

This is a super simple function that takes in two parameters, `num1` and `num2` and adds them, storing that value in a variable we declare inside of the function called `result`, then we return that `result`.
This is how it could be used in practice:

	console.log("2 + 5 is " + addTwoNumbers(2, 5));
	
Sure, not super useful, since we could just handwrite that code just as fast as calling the function. However, as your computations or logic gets more complex, you need to organize it into functions, lest you wish to go insane. Here is a good example of this:

	function raiseToPower(num, exponent) {
		var result = 1;
		for(var k = 0; k < exponent; k++) {
			result *= num;
		}
		return result;
	}

This function is a bit more complex than just adding two powers, because as you might be able to tell, it raises a `num` to an `exponent` and returns that `result`. This is still a fairly simple example, but you can see how it would be necessary to have a function like this rather than rewriting the tedious code everytime you wanted to use it. 

### Part 5: Simple DOM for your Dome

So far we have only been manipulating variables we have created in our Javascript file, with no real effect on our webpage. DOM, which stands for the Document Object Model, solves this! DOM allows us to interact with our HTML elements so we can change our webpage from Javascript! Let's take a look at a few examples:

index.html
	
		<!DOCTYPE html>
	<html>	
		<head>
			<title> Javascript Tutorial </title>
		</head>
		<body>
			<!-- NEW STUFF -->
				<div id="myDiv"></div>
				<div class="coolClass"></div>
				<div class="coolClass"></div>
			<!-- END OF NEW STUFF -->
			<script src="main.js"></script>
		</body>
	</html>
	
main.js

	var myDivVariable = document.getElementById("myDiv");
	var theCoolClassVariable = document.getElementsByClassName("coolClass");
	
	myDivVariable.innerHTML = "Hello, folks!";
	
	for(var k = 0; k < theCoolClassVariable.length; k++) {
		theCoolClassVariable[k].innerHTML = "This is a part of the cool class";
	}
	
	document.body.style.backgroundColor = "red";
	document.body.style.color = "white";
	
A lot to unpack here. The first thing we notice are these two variables we created: `myDivVariable` and `theCoolClassVariable`. These each store the value returned by a built-in DOM function. `document.getElementById(id)` returns the element that matches that id from the HTML file. In this case, we would return the `div` with an `id` of `myDiv`. The next DOM function, `document.getElementsByClassName(name)` returns an `array` of all the elements whose class matches that name. Essentially, an array is a data type that can store multiple values, and you can access those values by using square bracets `[index]` where the `index` starts at `0` and goes up to the `array.length - 1`, whatever that may be. Before we move on, here is a quixk example of arrays:

	var myList = ["hello", "my", "name", "is", "fred"];
	var fullSentence = "";
	for(var k = 0; k < myList.length; k++) {
		fullSentence += myList[k] + " ";
	}
	console.log(fullSentence);
	
	console.log("The first word is " + myList[0]);
	console.log("The last word is " + myList[4]);
	
	
Try running this example and see the output. Arrays can also store numbers, booleans, or objects like our DOM function `document.getElementsByClassName` returns.

Now, back to the DOM example.

The property `innerHTML` of a DOM object allows us to manipulate whatever is inside of the tags. We could even add in another HTML element with this! 

	document.body.innerHTML += "<div id='yolo'></div>";
	document.getElementById("yolo").innerHTML = "yolo div";
	
This is an easy way of manipulating our DOM, but not the best. It gets messy writing HTML is Javascript as a string. Notice that when we added the `div` with `innerHTML` and gave it an `id` we had to use `''` single quotes instead of `""` double quotes. This is because using two sets of double quotes would confuse the Javascript engine and give us an error. Theres a better way to create and add DOM objects in Javascript that we will go into in a moment.

The next thing we need to unpack is the `style` property of our DOM objects. We were able to manipulate the CSS of our HTML objects using this `style` property. 

CSS

	div {
		background-color: red;
	}
	
Javascript

	myObject.style.backgroundColor = "red";
	
These two statements, written in different languages, do the same thing, assuming they are both pointing to the same object. Take note of the syntax differences between them, like how in Javascript there aren't any `-`'s and instead the first letter of the next word is capitalized. This practice is called camelCase.

Now, onto the cleaner creation of HTML elements in Javascript. We saw how we could do this with `innerHTML`, but the better, more elegant way is with `document.createElement`. Here is an example:

	var myDiv = document.createElement("div");
		myDiv.style.backgroundColor = "red";
		myDiv.style.width = "100px";
		myDiv.style.height = "100px";
		
	var text = document.createElement("p");
		text.innerHTML = "Created with JS";
		
	myDiv.appendChild(text);
		
	document.body.appendChild(myDiv);
	
This creates two elements with the `document.createElement(elementName)` function. Then we can apply our DOM properties to those in order to change their style/text. Then, using `appendChild`, we add first the `text` element to `myDiv` and then append `myDiv` to our `document.body`. This is the equivalent of the following:

HTML 

	<body>
		<div style="background-color:red; width: 100px; height: 100px"> 
			<p>Created With JS</p> 
		</div>
	</body>
	
	
### Conclusion

Congratulations! You have succesfully learned the basics of Javascript. This will provide you with a base to start the rest of your learning. Check out the other projects we have on SDCoding to learn more. Get creative! The hardest part about programming is not remembering the syntax, that comes with practice, it's being able to use logic and creativity to solve problems and create new things.
