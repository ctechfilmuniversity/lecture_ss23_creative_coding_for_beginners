name: inverse
layout: true
class: center, middle, inverse
---

# Creative Coding for Beginners
### Film University Babelsberg KONRAD WOLF

Prof. Dr. Lena Gieseke | l.gieseke@filmuniversitaet.de 

---
layout:false

## Today



???
.task[COMMENT:]  

* TODO: Algorithmic Thinking Example?


--

* Re-Cap

--
* The Jumping Game

--
* Course Summary

--
* Follow-Up Topics

--
* Administration

---
template:inverse

# Libraries


---

## Libraries

--
* Extend p5 regarding specific topics

--
* Have its own documentation

--
* Might vary in quality
  
--
  
You must link a library file in your `index.html`

```html
<script src="path"></script>
```

--

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.6.0/p5.js"></script>
```

--

```html
<script src="p5.scribble.js"></script>
```

  
---

## The Sound Library

[p5.sound](https://p5js.org/reference/#/libraries/p5.sound)

--

Loading a sound file:

```js 
let song;

function preload() {
    song = loadSound('song.mp3');
}
```

--

```js
song.playMode('restart');
song.setVolume(0.1);
song.play();

...

if(song.isPlaying() == true){
    song.stop();
}
```
---
template:inverse

# Project File Organization

---
## Project File Organization

--
* Split the code into different files

--
    * Based on abstracted entities, e.g. *player*, *background*, *coin*
--
* In the p5 Editor: `Sketch Files` -> `Create File`
  

--
  
You must link a library file in your `index.html`


```html
    <script src="sketch.js"></script>
    <script src="background.js"></script>
    <script src="player.js"></script>
    <script src="coin.js"></script>
```

--

This is exactly the same as having all code in one file.

---
template:inverse

# The Jumping Game

--

### [[The Jumping Game Solution →]](https://editor.p5js.org/legie/sketches/5XhKQYG90)


---
## The Jumping Game

---
.header[The Jumping Game]

## Task 08.02 - Jumping

* `jumping` becomes true when the up arrow is pressed
* `jumpHeight` tracks the current jumping height of the player 
* `jumpStrength` tracks the value added `jumpHeight`
* constant `gravity` reduces `jumpStrength` in each frame

---
.header[The Jumping Game]

## Task 08.02 - Jumping

```js
function keyPressed() {

    if (keyCode == UP_ARROW) {

        jumping = true; 
        jumpStrength = jumpStrengthMax; 

    }
}
```

---
.header[The Jumping Game]

## Task 08.02 - Jumping

```js
function animatePlayer() {

  // The jumping
    if (jumping) {

        //jumpStrength *= 0.99;
        jumpStrength -= gravity;
        jumpHeight += jumpStrength;

        if (jumpHeight <= 0) {
            jumping = false;
            jumpHeight = 0;
            jumpStrength = 0;
        }
    }

    playerY = playerYOnGround - jumpHeight;
}
```

[[Jumping Game Step 04 - The Jumping - Solution →]](https://editor.p5js.org/legie/sketches/xEyouFkwg)

---
.header[The Jumping Game]

## Task 08.04 -  Counting Coins

`gameFont` saves the font used for the text display:

```js
let gameFont;

function loadGameFont() {
  
  gameFont = loadFont('ka1.ttf');
}

function initGameFont() {
  
    textFont(gameFont);
    textAlign(CENTER, CENTER);
}

```

---
.header[The Jumping Game]

## Task 08.04 -  Counting Coins


`coinCollectedNumber` counts the number of coins collected: 


```js
// Check for collision between coin and player:
if (dist(coinX, coinY, playerX, playerY) <= 
        playerImg[1].height * 0.5 + coinSize * 0.5) {
    
    coinCollected = true;
    coinCollected++;

    ...
}
```

--

```js
function displayCoins() {
    image(coinSmallImg, 10, 10);
    fill(0, 0, 0);
    textSize(20);
    text(coinCollectedNumber, 49, 19);
}
```


[[Jumping Game Step 05 - Coins Collected - Solution →]](https://editor.p5js.org/legie/sketches/ZvfdkS_G7)

---
.header[The Jumping Game]

## Task 08.05 - Game Over 


--

### First Enemies

Almost identical to `coins.js`.


???
.task[COMMENT:]  

* https://editor.p5js.org/legie/sketches/GpW1kUaTB

---
.header[The Jumping Game]

## Enemies

Two types of collision

* If the player is walking or jumping up, then the player dies
* If the player is coming down from a jump, then the enemy diese

--

```js
  if (dist(enemyX, enemyY, playerX, playerY) <=
      playerImg[1].height * 0.5 + enemySize * 0.5) {
    
    
    if (jumpStrength < 0) {
      enemyDead = true;
      
    } else if (!enemyDead) {
      
      gameOver = true;
    }
    
  }
```

[[Jumping Game Step 06 - Enemies - Solution →]](https://editor.p5js.org/legie/sketches/GpW1kUaTB)

---
.header[The Jumping Game]

## Task 08.05 - Game Over 

```js
// Game Logic
let gameOver = false;
```

Is set to true when colliding with an enemy while walking.

```js
function displayGameOver() {

    // The "game over" text
    fill(255, 0, 0);
    textSize(42);
    text("Game Over", width * 0.5, height * 0.5 - 50);
}
```

---
.header[The Jumping Game]

## Task 08.05 - Game Over 
```js
function draw() {
  
	animateBackground();
	displayCoins();
	animatePlayer();
	
	if (!gameOver) {
		
		animateCoin();
		animateEnemy();
		
	} else {
		
		displayGameOver();
	}
 
}
```

---
.header[The Jumping Game]

## Task 08.05 - Play Again?

---

```js
function displayGameOver() {
	
	// The "game over" text
	fill(255, 0, 0);
	textSize(42);
	text("Game Over", width * 0.5, height * 0.5 - 50);
	
	// The "play again" text
	let textPlayAgain = "Play Again?";
	let textPlayAgainW = textWidth(textPlayAgain);
	let textPlayAgainX = (width * 0.5) - textPlayAgainW * 0.5;
	let textPlayAgainY = height * 0.5;

	// Is the mouse on the text?
	if (mouseX > textPlayAgainX && mouseX < textPlayAgainX + textPlayAgainW &&
		mouseY > textPlayAgainY && mouseY < textPlayAgainY + 50) {
		fill(255, 165, 0);
		
		// Restart the game if the mouse is clicked
		if(mouseIsPressed){
			
			gameOver = false;
			coinCollectedNumber = 0;
			setup();
		}
	} else {
		fill(0, 0, 0);
	}

	textSize(32);
	text(textPlayAgain, width * 0.5, height * 0.5);
}
```

---
.header[The Jumping Game]

## Task 08.05 - Play Again?

```js
function initBackground() {

    ...

    bgSound.setVolume(0.1);
    bgSound.playMode("restart"); // WAS MISSING
}
```

--

[[Jumping Game Step 07 - Game Over - Solution →]](https://editor.p5js.org/legie/sketches/1oCVIa10x)

---
.header[The Jumping Game]

## Bird Enemies

[[Jumping Game Step 07 - Bird Enemies - Solution →]](https://editor.p5js.org/legie/sketches/5XhKQYG90)



---
template: inverse

# Course Summary


---
.header[Course Summary]

## Commands

* Functions define functionality blocks within `{}`
    * Commands are *function calls*.
--
* You can define what should happen in given functions, e.g., `setup()`

--
* You can write your own functions and call them

```javascript
function functionname([parameter1,...]) {

    // Code that is executed when we call the function

    [return value;]
}
```

---
.header[Course Summary]

## Program Flow

* p5's environment
    * `preload()`
    * `setup()`
    * `draw()`
--
* Structuring the program flow
    * `if(condition is true)`
    * `while(condition is true)`

--

## User Input

* User Input from
    * `keyPressed()`
    * `mouseX`, `mouseY`

---
.header[Course Summary]

## Variables

We use variables to save and access data

--
* `let hue = 0;`
    * Variables have a data type
    * Variables live inside `{}` and have a scope


--

## Operators

* Arithmetic
    * `+`, `-`, `*`, `/`, `--`, `++`
* Comparison
    * `>`, `>=`, `<`, `<=`, `==`, `!=`
* Logical Operators
    * `&&`, `||`, `!`

---
.header[Course Summary]

## Color Systems

* Two color systems available
    * RGBA
    * HSB
    * `colorMode(HSB);`
    * `colorMode(HSB, windowWidth, 100, 100);`

---
.header[Course Summary]

## Loops

```js
while(i < numberOfTimes)…
```

```js
for(int i = 0; i < numberOfTimes; i++)…
```

--

2D Loop

*For every row look at every element…*

```js
for (let y = 0; y < numberRows; y++)
{
    for (let x = 0; x < numberColumns; x++)
    {
        print("Row: " + y + " Column: " + x);
    }
}
```

---
.header[Course Summary]

## Objects

* Have properties and functions that *belong to* them
* You access those properties and functions with the `.` notation
    * `myImage.width`
    * `myImage.resize(100, 100);`
--
* p5.Image, p5.sound, arrays


---
.header[Course Summary]

## Arrays

With arrays we can save multiple values in one variable.

--

```js
let myArray = [2, 4, 6, 8, 'done']

myArray.push(100) // -> [2, 4, 6, 8, 'done', 100]
myArray[1] = 'hello' // -> [2, 'hello', 6, 8, 'done', 100]
```

--

Arrays are accessed with `[]` and an index, starting at `0`.

--

```js
print(myArray[2]) // 6
```

--

You can use loops to access all elements of an array.

```js
for (let i = 0; i < myArray.length; i++) {
    print('Element', i, ': ', myArray[i]);
}

//or

for (let element of myArray) {
    print(element);
}
```

---
.header[Course Summary]

## Images

```js
let imgPanda;

function preload() {
    imgPanda = loadImage("panda.jpg");
}

function draw() {
    image(imgPanda, 50, 50);
}
```

--

* Animate images e.g. by changing their position like any other shape
* Store images in arrays and display them sequentially to animate image series
* Use `get(x, y)` and `set(x, y, color)` to return or set the color of the image at a specific pixel


---
.header[Course Summary]

## Libraries

* Libraries extend the p5 library in regard to one specific topic.
* You have to activate a library for a sketch in openProcessing.  
* For knowing how to use a library you have to refer to the library's given documentation, it is not necessarily on the p5 page.  
  
--

[p5.sound](https://p5js.org/reference/#/libraries/p5.sound)

--

Loading a sound file:

```js 
let song;

function preload() {
    song = loadSound('song.mp3');
}
```

--

```js
song.playMode('restart');
song.setVolume(0.1);
song.play();

...

song.stop();
```

---
template:inverse

# Use the [reference](https://p5js.org/) 🚒


???
.task[COMMENT:]  

* https://happycoding.io/tutorials/p5js/


---
## Code Organization

--

* Good layout matters!!

--
* Write your own functions
* Split your code into different files

---
## Algorithmic Thinking

--

The goal is an **algorithm** that defines a list of steps to finish a task.

.footnote[[[code.org]](https://code.org/curriculum/course3/1/Teacher)]

--
  
* **Decomposition**: Break a problem down into smaller pieces

--
* **Pattern Matching**: Find similarities

--
* **Abstraction**: Reduce specific differences and make one solution work for multiple cases

---
.header[Course Summary]

## Learning Objectives

With this course, you hopefully gained

--
* An understanding of programming

--
* **Skills to develop simple programs from scratch**
    * Knowledge about resources
    * Guidance towards and learning through self-studies
--
* Skills to apply programming as (an expressive) tool


???
.task[COMMENT:]  

* But it is like a poetry class in Japanese

---
template:inverse

# Follow-Up Topics

---
.header[Follow-Up Topics]

## Coding Environments

For now, it is perfectly fine to continue with coding on the p5 Editor.  


???
.task[COMMENT:]  

* For each sketch you can control to whom the sketch is visible. With the option "Anyone can see your sketch" anyone with the URL can see your results - which is very handy of you want to share your work.

--
* Eventually you should move on to a more flexibel environment, e.g., a text editor

--

I like [Visual Studio Code](https://code.visualstudio.com/) (in short VSCode). The editor is

* Free
* Multi-purpose
* Extensively adjustable

???

I like it because I can write different types of languages with it while still having many language specific features. Also, I am totally addicted to customizing my working environments to exactly the way I like it and VSCode let's me do so in a convenient way (enabled through *extensions*). In summary, it is:

---
.header[Follow-Up Topics]

## Coding Environments

But how can you develop and run a website on you local computer?

???

This will need a bit more learning on your side.

--

### Local Webserver

With a so-called local webserver you can build a "mini-Internet" on your computer. That is what professional web developers do, when working on a website.

--

The workflow would be:

* Write code on your computer, e.g. with Visual Studio Code
* Start a webserver
* Look at the results in a browser

???

.task[TASK:]  

* Download game
* Start VSCode webserver
* Make it run locally

---
.header[Follow-Up Topics]

## Object Oriented Programming

--

```js
let myVector;

function setup() {
    createCanvas(300, 300);
    myVector = new p5.Vector(150, 200);
}

function draw() {
    background(50);
    circle(myVector.x, myVector.y, 100);
}
```

--
Creating object instances with `myInstance = new Classname();`

---
.header[Follow-Up Topics]

## Object Oriented Programming

Bad:

```
let positionX = [];
let positionY = [];

let stepX = [];
let stepY = [];
```

--
Good:

```
let confetti = [confettoObject1, confettoObject2, confettoObject3,...];

...
confetti[0].x
confetti[0].y
confetti[0].stepX
confetti[0].stepY
confetti[0].hue
confetti[0].size
```

Create your own objects!



---

## Follow-Up Topics

* Video

???
.task[COMMENT:]  

* Mention video, show https://p5js.org/examples/dom-video-capture.html

--
* Machine Learning with ml3

--
* Sound?

--
* 3D?

--
* Web Development?

--
* Data Visualization?

---
template: inverse

# Where Should You Go From Here?
# 🤔

---

## Where Should You Go From Here?

--
* Do the final project

--
* Pick a direction you want to focus on
    * Generative designs
    * Games
    * Tools
    * etc.
--
* Watch tutorials and courses

--
* Look through other people's and professional code

--
* Create your own projects

---
## Where Should You Go From Here?

Once you stop to practice coding you will lose the skill. 😨 

--

But it will come back much faster once you are coding again! 😁


---
## Where Should You Go From Here?

I am happy to advise projects, theses, etc.  
  
Just get in touch.

---
template:inverse

# Administration

---
## Administration


### 2 SWS + X ECTS

* 1 ECTS for attending the lectures 
* 2 ECTS for completing 70 % of the homework assignments 
* 1-3 ECTS for the final project

---
.header[Administration]

## Homework

You can hand in homework until **July 28th** to make it count. This is a hard deadline.

---
.header[Administration]

## The Final Project

You can do anything you like as a final project. 

--

You have to hand in the final project in your Owncloud file until **September 30st**. This is a hard deadline.

--

Moreover, submit at least one representative image and a short project description covering the following aspects:

* Concept
* Implementation
* Results
* Lessons Learned
* Time spent on the project
  
--
  
Feel free to get in touch with me before or during your work for any additional questions.

---
## Administration

> Let's do the evaluation!



---
template:inverse

## The End

# 👋🏻

