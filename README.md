# The story so far…
Yesterday, my son said he wanted to.. “Learn to Code like Dad”.

Excited, I imagined him sitting at a terminal console, hacking code with occasional yelps of glee when he got something working. For a moment, I had high hopes and dreams.

Many years ago, I learn to program by sitting down and reading C Programming from K & R. Probably not the best reference today for a 10 year old. He had already done tons of the Scratch demos and Code.org demos, but I felt the need for something a little more “native” that wasn’t a website with a “Next >> Next >> Done” Wizard.

I wrecked my brains on where to start that would give hime immediate wins. Something like Visual Basic or WinForms I though, but what is current and useful in the “Interwebs” today for a 10 year old? Not C, Not C# (even if it’s my favourite language), Definitely not Java. Python seems like a good starter, but I really want him to have the power to use something that gave visual feedback. Javascript seems a little to daunting and frankly, I think it sets up bad practices and frustrations for beginners, but what else was there?

Eventually, I settled on a niche: Javascript + HTML5 Canvas, but I wanted to make it a little more simple, and this is when I found EaselJs. There was even a really great demo of the classic Asteroids game. I showed it to him, and he was excited. We got the code working locally, and I showed him the code – about 450 lines of code..

His first reaction:

“Oh My God, That’s a Lot of Code!”, he said with a worried tone.

I have to be honest, my thoughts were the opposite…

Then it hit me. What if I could strip back this Asteroids Game to the most simple concept, with the least amount of lines of code, and build it out into the classic game, or maybe have the game morph into another game.

I did an initial cut to 200 lines, and removed all the Asteroids, so there was only a ship that could rotate and thrust forward. The Whole Game was 118 Lines of Code (Abet, the Ship.js was another 118 lines of code). I showed it to him. He was genuinely excited.

“Dad, Can you make the ship go at Warp Speed”,

“I don’t know, let’s find out”.

We jumped in a looked for what we could tweak. First Attempt, we altered the `Ship.MAX_THRUST`, so we got greater acceleration, but not greater max velocity. He spotted the max velocity parameter.

“What if we change that“, he asked excitedly

We tweaked the `Ship.MAX_VELOCITY` from 5 to 50, and voila – we had warp speed.

He was in stitches laughing.

In 50 minutes, he had discovered the power of hacking. He was empowered, I was excited. Something was happening…

Just to put this in context, this is not the first time he has looked at code. We have played with GitHub, Code.Org, Raspberry PI, and event basic html web development before, but nothing made him excited, as it all just seems like too much overwhelm, and no immediate progress.

This time it was different.

This all happened because I’ve decided to spend 1 hour a day (even though I have an incredible busy schedule), playing with code, so I’ve committed to #100DaysOfCode.

This is Day 3 of #100DaysOfCode for me.

My Plan is now to break this down to simple steps that any 10 year old kid could follow (with their Dad), and have fun while learning the Power of Code.

It might not change the world, but for today, at least, it feels like it could make a difference in my son’s life.

If you come across this page, and like what you see, please let me know, Feedback is the breakfast of champions, so if you like what you see, it will inspire me to keep doing this.

# Let’s begin…
Start by Cloning the repo below and run the original Game from EasleJS. See what you think. It’s pretty awesome. You can find it in the `Game` folder.

Next Look at [01-Game.html](https://www.colhountech.com/Asteroids2D/01-Game.html), and read [01-README.md](01-README.md)

This will evolve and change as I learn more…