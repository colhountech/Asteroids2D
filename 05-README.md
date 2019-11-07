# Spin an Asteroid

Today, we are going to add some spin to the asteroid.

First, let's define the amount of spin we add to the asteroid for each tick. In the Rock function, add a new variable
called `spin`

```js
    this.spin = 1.0;
```

Once, again to keep things simple, we will spin the Asteroid by 1 radian each time.

Next, we will add a `tick()` function to our `Rock()`. In this function, we change the `rotation` of the Rock as
follows:

```js
    this.tick = function (event) {
        this.shape.rotation += this.spin;
    }
```

All we need to do then is to tell the stage to also call the tick function every time we update the Ship. We do this at
the very end of the tick event for our game.

```js
    ship.tick(event);
    rock.tick(event); // Add this new line
    stage.update(event);

```

That's it. Now when you save and reload the game,  you should see a rotating asteroid. See [05-Game.html](05-Game.html) for the finished version.

See you tomorrow

