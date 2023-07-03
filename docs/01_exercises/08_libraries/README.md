---
layout: default
title: Exercise 08
parent: Exercises
nav_order: 8
---

# Creative Coding For Beginners
  
Prof. Dr. Lena Gieseke \| l.gieseke@filmuniversitaet.de  
  
  
# Exercise 08 - The Jumping Game

This session is due on **Monday, July 10th**.  


---

* [Creative Coding For Beginners](#creative-coding-for-beginners)
* [Exercise 08 - The Jumping Game](#exercise-08---the-jumping-game)
    * [The Jumping Game](#the-jumping-game)
    * [Task 08.01 - The Code Base](#task-0801---the-code-base)
    * [Task 08.02 - Jumping](#task-0802---jumping)
        * [Convenience - Adding a "On the Ground" Variable](#convenience---adding-a-on-the-ground-variable)
        * [Adding the Jumping Status](#adding-the-jumping-status)
        * [The Jumping Up](#the-jumping-up)
        * [The Coming Down](#the-coming-down)
        * [Landing](#landing)
        * [Cosmetics - Reducing The Jumping Strength](#cosmetics---reducing-the-jumping-strength)
    * [Task 08.03 - Displaying The Jumping Image](#task-0803---displaying-the-jumping-image)
    * [Task 08.04 -  Counting Coins](#task-0804----counting-coins)
    * [Task 08.05 - Game Over (Optional)](#task-0805---game-over-optional)


## The Jumping Game

You can download all [assets for the game](https://owncloud.gwdg.de/index.php/s/zP886Q6p4wob5on).

## Task 08.01 - The Code Base

Use [Step 03 - Structure](https://editor.p5js.org/legie/sketches/2nuJGEvFr) as starting code. First, look through the code and try to understand all code.

## Task 08.02 - Jumping

Now, we will implement the jumping of our little player guy. 

The result of this task should look like (use the up arrow key to jump):

<iframe src="https://editor.p5js.org/legie/full/xEyouFkwg"></iframe>

If you want a challenge, try to implement the guy's jumping on your own.  

Otherwise you can put together the following given steps. The following gives you all the steps needed for implementing the jumping. You simply need to put it together. But do not simply copy and paste - also try to really understand each step!

### Convenience - Adding a "On the Ground" Variable

Currently, we are computing the y-position of the player once in `initPlayer` with

```
playerY = height - playerImg[1].height - bgHeightOffset;
```

Because we are using the value of the player being on the ground over and over again, let's save it in a global variable. Then the system only needs to compute the value once and we reuse it after that through the variable.

```js

...
let playerYOnGround = 0; // We need this position over and over again, so let's save it

function initPlayer() {

    // Place the player
    // at the middle of the screen in width...
    playerX = width * 0.5 - playerImg[1].width * 0.5

    // ...and at the bottom in height.

    // The bottom of the canvas equals height
    // and we need to move up the playerSize
    // and some offset to that match the background image
    playerYOnGround = height - playerImg[1].height - bgHeightOffset;
    playerY = playerYOnGround;
}
```


### Adding the Jumping Status

Now, we want to add the key input for activating the "jumping". For that we add a global variable jumping, which is either false, if we are not jumping, or true, when we are jumping. We set that variable in a keyPressed() function and check for its value in draw (where we eventually want to do the jumping - which is adjusting the position of the player).

For the up arrow we need the system variable `keyCode` for special keys. You can find it in the [reference](https://p5js.org/reference/#/p5/keyPressed).

```js

...

// Jumping Variables
let jumping = false; // Are we currently jumping? Set to true while the player is jumping

...

function animatePlayer() {

    ...

    if (jumping) {      
        print("We started to jump");
    }
    ...
}


// Key input for controlling the jump:
// the up-arrow key makes the
// player jump
function keyPressed() {

    if (keyCode == UP_ARROW) {

        jumping = true; // This will trigger to compute the jumping movement in setup()
    }
}

```

### The Jumping Up

The actual jumping works as follows: we have a variable `jumpHeight`, which tracks the current jumping height of the player in each frame and a variable `jumpStrength`, which tracks the value that we want to add to the jumpHeight (similar to step for the previous circle animation example) in each frame. The jumping is then computed in each frame by adjusting the jumpHeight with jumpStrength and subtracting the `jumpHeight` from `playerYOnGround` to get the final postion.

Also, we add the global variables jumpStrengthMax, which is a constant value for controlling the initial speed of the jumping.

```js
...

// Jumping Variables
let jumping = false; // Are we currently jumping? Set to true while the player is jumping
let jumpHeight = 0; // The current height of the player in each frame
let jumpStrength = 0; // Value that we add the the player's position for the jumping
let jumpStrengthMax = 5; // Constant value, controlling the speed of the jumping


...


function animatePlayer() {


    if (jumping) {
        jumpHeight += jumpStrength;
    }

    playerY = playerYOnGround - jumpHeight;

}

function keyPressed() {

    if (keyCode == UP_ARROW) {

        jumping = true; // This will trigger to compute the jumping movement in setup()
        jumpStrength = jumpStrengthMax; // Start the jump with maximal strength
    }
}
```

Now, the player should move up when we press the up arrow.

### The Coming Down

We need to make sure that the player also comes down at some point. So, we need to make the value jumpStrength negativ at some point. With a negativ value, the direction of the movement is reversed and the player moves down again. For that we add the constant global variable `gravity` and subtract `gravity each frame from jumpStrength. Then at some point jumpStrength will become negative and the direction of the jump in reversed.


```js
...

let gravity = 0.1;

...


    if (jumping) {
        jumpStrength -= gravity;    
        jumpHeight += jumpStrength;
    }
    playerY = playerYOnGround - jumpHeight;

...
```

Now, the player should move back down again at some point after the jump.


### Landing

For making the player's coming down stop at the ground, we add a check whether `jumpHeight <= 0` (which it is when the player is back on the ground) and set `jumping` to `false` and `jumpHeight` and `jumpStrength` to zero. Then the jumping activity is over.


```js
    if (jumping) {
        jumpStrength -= gravity;    
        jumpHeight += jumpStrength;

        if (jumpHeight <= 0) {
            jumping = false;
            jumpHeight = 0;
            jumpStrength = 0;
        }
    }
```

### Cosmetics - Reducing The Jumping Strength

Usually a "force" such as `jumpingStrength` is slightly reduced each frame to further slow the movement down. Adding a small factor to slow down the movement makes it look more natural. However, this step is really just cosmetics. We can make the movement look anyway we want.

```js
    if (jumping) {
        jumpStrength *= 0.99;   
        jumpStrength -= gravity;    
        jumpHeight += jumpStrength;

        if (jumpHeight <= 0) {
            jumping = false;
            jumpHeight = 0;
            jumpStrength = 0;
        }
    }
```


*Submission*: Add a link to your sketch in your OwnCloud file.


## Task 08.03 - Displaying The Jumping Image

There is actually a different image for the little guy when he jumps.

Try to implement the displaying of a different image for when the guy is jumping on your own. Specifically, use `guy-4.png` for the jump.

If you don't get anywhere, follow the code below. Since we already have a boolean "jumping", we only need to write a simple `if...else` clause.

```javascript
// Chosing which player image to
// draw based on the current
// player activity
if(jumping){

	image(playerImg[4], playerX, playerY)
	
} else {
    
    // Walk cycle
	image(playerImg[playerImgIndex], playerX, playerY);

	// Walk images are images 0..3
	// We want to iterate the walking image for each draw call.
	// For that, we count up playerImgIndex up until 3
	// and then back to 0

	if (frameCount % animationSlowDown == 0) { // Every 8th frame
		playerImgIndex++; // Next image

		if (playerImgIndex > 3) { // Reached last walk cycle image
			playerImgIndex = 0 // Back to first image
		}
	}
}
```

*Submission*: Add a link to your sketch in your OwnCloud file.


## Task 08.04 -  Counting Coins

The goal of this task is to display the number of coins selected as text on the screen. For that

* add a variable that counts the number of coins selected so far by the player,
* look up how to add [text](https://p5js.org/reference/#/p5/text) ([reference](https://p5js.org/reference/#group-Typography), [examples](https://p5js.org/examples/)) to a canvas, and
* display that number as text on the screen, e.g. in the upper left corner.

*Submission*: Add a link to your sketch in your OwnCloud file.

## Task 08.05 - Game Over (Optional)

Create some logic that sets the game to a *game over* state at some point. Whether this is after one collision with the enemy or after a number of collisions is up to you to decide. It is also up to you what should happen then. You could stop the game and display text or also even just restart the game.

*Submission*: Add a link to your sketch in your OwnCloud file.


---

*Happy Jumping!*
