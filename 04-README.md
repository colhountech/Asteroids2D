# Refactoring

There is only one secret to writing really good code and that secret is called __Refactoring__. This means that when you get your code to do what you want it to do, you still are not done... There is still some homework you need to do. 

Once you have a working piece of code that does something useful, a good software engineer will also take one more step. How do you take that working code and make it easlier to understand and easier to look after, so that when you come back later, your life is easier. __Refactoring__! 

__Refactoring__ is improving the code so that it is __elegant__ and __beautiful__. When you make your code __elegant__ and __beautiful__ you will really enjoy working on your code, and so will other people.

The opposite to clean, refactored code is called __Hacking__. Hacking is often the term used when you try to modify code that is hard to change, is hard to understand and makes your life frustrating, anoying and somtimes even desperate. 

When you get good at __refactoring__ your code, your life as a software engineer or software developer becomes a joy and you get excited when you think about adding new magic to your code. 

Let's take [03-Game.html](03-Game.html) and do a little __refactoring__ to make it more __elegant__.

Look at lines 51-68 below:

```js
		// create a rock
		let size = 40;
		let radius = 0;
		let angle = 0;

		let rock = new createjs.Shape();
		rock.graphics.clear();
		rock.graphics.beginStroke("gray");
		rock.graphics.moveTo(0, size); // start at bottom of the rock

		while ( angle < 6.0 )
		{
			angle += .25 + (Math.random() * 100) / 500;
			radius = size + (size / 2 * Math.random());
			rock.graphics.lineTo(Math.sin(angle) * radius, Math.cos(angle) * radius);
		}
		
		rock.graphics.closePath(); // draw the last line segment back to the start point.

```

We have 17 lines of code here that really only do one thing - these lines create the shape of the rock.

Remember `function`s? Wouldn't it be much more elegate if we hid this code inside a single `function` and then we make our code more elegant. If we create a function called `Rock()` and move all the code inside this, we can then replace all this code with a single line like this:

```js
    var rock = new Rock();
```

Here is our new function. It's almost exactly the same, we have just moved the code around. 
```js

    function Rock() {

		const size = 40;
		let radius = 0;
		let angle = 0;

		this.shape = new createjs.Shape();
		this.shape.graphics.clear();
		this.shape.graphics.beginStroke("gray");
		this.shape.graphics.moveTo(0, size); // start at bottom of the rock

		while ( angle < 6.0 )
		{
			angle += .25 + (Math.random() * 100) / 500;
			radius = size + (size / 2 * Math.random());
			this.shape.graphics.lineTo(Math.sin(angle) * radius, Math.cos(angle) * radius);
		}
		
		this.shape.graphics.closePath(); // draw the last line segment back to the start point.
	}
```

Todays Task is to take [03-Game.html](03-Game.html) and modify it to match [04-Game.html](04-Game.html) by refacoring the code above into a new function called `function Rock()`.

Tomorrow, we are going to start to make the rock move. See you then.




