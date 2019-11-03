# 01-Game

Open  [01-Game.html](01-Game.html) in your browser, and the game should load.

To begin with, this is the simplest game we can build.

Pay attention to the following:
```html
	<body onload="init();">
```

When the page is loaded, `init()` is called. That's the next block of code we will look at.

`gameCanvas` is the Canvas where our Game is drawn. In our game it's the black background. This tells us how big we want our display, usually this would be the size of the full screen for a game. You can see here it's `black`. Try changing it to `navy`.

In our Asteroids Game, we have 3 important "things"  or "objects" (I much prefer "things" than "objects", but aparently "objects" won, and that'w what most people use to call "things" in code). So, the 3 important objects are: 

* A `canvas` which is what we can see on the screen.
* A `stage` is where everything goes before it's drawn on that canvas. 
* A `ship` which we will add to the stage and move around the stage so we can see it on this canvas. 

All easy so far? Good.

So, we are using a toolkit called  `EaselJs` and with this we will add the `ship` to the `stage` and move it around the `stage` and then EaselJS will draw this on our `canvas` display for us, so we don't have to get caught up on yucky code  :)


You can see where we define these 3 things below:
```js
	var canvas;			//Main canvas
	var stage;			//Main display stage
	var ship;			//the actual ship
```


See this line?
```js
<script type="text/javascript" src="Ship.js"></script>
```
To keep things simple, we have already have the code for the Ship in a different file - `Ship.js` so for now, we just accept that the ship knows how to draw itself and move. we just want to give it commands to move around based on the keys we press. If you are really curious (and  you should be), you can have a peek at the [Ship.js](Ship.js) file and play with the `MAX_VELOCITY` or `MAX_THRUST`, See what happens to our game.

Next we need to define what commands are going to move our ship. Let's use the arrow keys and we will define these too in code. Every key on the keyboard has a special code, so rather than trying to remember these codes, we will just give them nice easy to remember names:

```js
	var KEYCODE_UP = 38;		//useful keycode
	var KEYCODE_LEFT = 37;		//useful keycode
	var KEYCODE_RIGHT = 39;		//useful keycode
```

Computers can read the Key Codes very quickly in a fraction of a second, so we also need to check if the keys are being held down or being released.  We only will move the ship if the key is being held down. when a key is pressed we will activate a command and when a key is released, we will deactivate a command. 

We have 3 commands that we will map to keys:

```js
	var cmdLeft;				//is the user holding a turn left command
	var cmdRight;				//is the user holding a turn right command
	var cmdForward;			    //is the user holding a forward command
```

The next 2 lines needs a little bit of explaination. Have you ever put on some toast, and asked Alexa to set a timer for you to remind you to check that your toast is done. You might say:

>"Hey, Alexa! Set a timer for 2 minutes"

In 2 minutes, Alexa comes back and starts to ring an alarm. Very useful so you toast doesn't get cold.

In code, we call these alarms funny names called **Handlers** because they handle alarms. They are just alarms that we can use to tell us something has happened, like a key was pressed down or a key was lifted up.

That what the next 2 lines are about:

```js
    //register key functions
	document.onkeydown = handleKeyDown;
	document.onkeyup = handleKeyUp;
```

* The first line tell us to run the `handleKeyDown` code whenever a key is being pressed down.
* The  next line tell us to run the `handleKeyUp` code whenever a key is being lifted up.

So, in our handler, all we need to do is check to see if one of our special command keys is being pressed: left arrow key, right arrow key and up arrow key. If we wanted to add more commands later (like a fire button), we would tell one of our handlers to check for this command too.

OK. That' pretty much it. Not much there. The rest of the code are blocks of code wrapped that we can use when we need. They are called `function`s and they all look like this:

```js
function restart() {
    // some code
}
```

A `function` really is nothing more than a label or name of a block of code. Just makes it easier to read and understand, and is one of the important bits behind being a good programmer - use `function`s.

OK. Let's look at the rest of the functions in our Game.

### init()

init always runs first when you load the webpage. so far it doesn't do much.

```js
    canvas = document.getElementById("gameCanvas");
	stage = new createjs.Stage(canvas);
    restart();
```
Pretty simple really? Just find the `canvas` to draw on. Create a `stage` and then `restart()` the game. Enough said.

### restart()

`restart()` is just a block of code that we will run every time we restart the game. This will be useful later when our game ends, and we don't need to reload the webpage to restart the game.

restart() only does 4 simple things at the start of our game: 

It clears the Stage of everything ready for a new game. In the code world, we usually call a thing that looks after other things as a `parent` and the things it looks after are `children`. In our game the only child will be a single ship, but later we will have other asteroids too, so all of these together are the `children` on the stage. I guess you could think of the stage really like a parent acting as a stage manager and it manages all the things on the stage such as ships and asteroids - it's children.

So, every time we start the game we need to remove all the children from the stage.

```js
	//hide anything on stage 
	stage.removeAllChildren();
```

Next, we add the Ship to the stage. We position it in the middle of the stage with is half the width and half the height of the canvas. 

`x` is how far along the left to right direction, and `y` is how far down the up to down direction, starting in the top left corner as `x = 0` and  `y = 0`.

```js
		//create the player
		ship = new Ship();
		ship.x = canvas.width / 2;
		ship.y = canvas.height / 2;

		//ensure stage is blank and add the ship
		stage.clear();
		stage.addChild(ship);
```
We also reset all the key presses. It's good practice to reset all our labels at the start of our game.

```js
		//reset key presses
		lfHeld = rtHeld = fwdHeld = dnHeld = false;
```
And Finally, we start the Game Timer. this is THE most important part of any realistic game. Sonetimes it's called the Game Loop and it's what gives us the `fps` number when we play games. for example, if a game has an `fps` of 100, that means it's running the Game Loop 100 times every second. 100 frames per second = 100 fps. You have probably heard about fps if you are a gamer. 

Every time the game loops code is called, it makes tiny change to our ship. Normally, we want our game loop to run at 24 times a second. Any faster than that and the human eyes doesn't really notice, unless if you have a very fast moving game like Fortnite or Black Ops. In these games, the higher the fps, the smoother the game looks when you move around. For our game we will let `EaselJs` look after the frame rate for us, which normally is 30 frames per second.

Here is how to setup the game loop:

```js
		//start game timer
		if (!createjs.Ticker.hasEventListener("tick")) {
			createjs.Ticker.addEventListener("tick", tick);
		}
```

That's everything. Now go back a read through the code and see if
everyting makes sense, and we are ready to start addding back some cool stuff to build out our game.


## tick()

`tick()` is our Game Loop. This is where all the magic happens in every Game like this. Our game is very simple right now, so we can see 2 things we need to check and 2 other bits of housework we need to look after.

 we need to rotate the ship left or right, 

//handle turning
		if (lfHeld) {
			ship.rotation -= TURN_FACTOR;
		} else if ( rtHeld) {
			ship.rotation += TURN_FACTOR;
		}
		//handle thrust
		if (fwdHeld) {
			ship.accelerate();
		}
		//call sub ticks
		ship.tick(event);
		
		// update stage
		stage.update(event);
