---
layout: default
title: Exercise 04
parent: Exercises
nav_order: 4
---

# Creative Coding For Beginners
  
Prof. Dr. Lena Gieseke \| l.gieseke@filmuniversitaet.de  
  
  
# Exercise 04 - Variables

This session is due on **Monday, June 5th**.  

* [Creative Coding For Beginners](#creative-coding-for-beginners)
* [Exercise 04 - Variables](#exercise-04---variables)
    * [Task 04.01 - Program Understanding](#task-0401---program-understanding)
    * [Task 04.02 - Code adjustment](#task-0402---code-adjustment)
    * [Task 04.03 - Inspiration](#task-0403---inspiration)


## Task 04.01 - Program Understanding

Execute and understand and explain the [following code](https://editor.p5js.org/legie/sketches/mfJiSQu4o).

Careful, you might need to look stuff up in the reference, e.g. [`constraint()`](https://p5js.org/reference/#/p5/constrain)and [short-cuts for arithmetic operators](../../02_scripts/ccfb_ss23_07_variables_script.md#arithmetic-operators)

```js
// Based on https://happycoding.io/tutorials/p5js/animation/bouncing-line

let lineStartX;
let lineStartY;
let lineEndX;
let lineEndY;

let stepStartX;
let stepStartY;
let stepEndX;
let stepEndY;
let rangeStep = 5;

let r;
let g;
let b;


function setup() {
    createCanvas(300, 300);

    lineStartX = random(width);
    lineStartY = random(height);
    lineEndX = random(width);
    lineEndY = random(height);

    
    stepStartX = random(-rangeStep, rangeStep);
    stepStartY = random(-rangeStep, rangeStep);
    stepEndX = random(-rangeStep, rangeStep);
    stepEndY = random(-rangeStep, rangeStep);

    r = random(255);
    g = random(255);
    b = random(255);

    noFill();
    strokeWeight(2);
    background(32);
}

function draw() {

    // Draw a line
    stroke(r, g, b, 80);
    line(lineStartX, lineStartY, lineEndX, lineEndY);
    // bezier(0, 0, lineStartX, lineStartY, lineEndX, lineEndY, width, height);

    // Increase the color values by a random number
    r += random(-2, 2);
    g += random(-2, 2);
    b += random(-2, 2);
    
    // Check the reference for the
    // constraint function!
    r = constrain(r, 0, 255);
    g = constrain(g, 0, 255);
    b = constrain(b, 0, 255);

    // Move the line a bit
    lineStartX += stepStartX;
    lineStartY += stepStartY;
    lineEndX += stepEndX;
    lineEndY += stepEndY;

    if(lineStartX < 0 || lineStartX > width){
        stepStartX *= -1;
    }

    if(lineStartY < 0 || lineStartY > height){
        stepStartY *= -1;
    }

    if(lineEndX < 0 || lineEndX > width){
        stepEndX *= -1;
    }

    if(lineEndY < 0 || lineEndY > height){
        stepEndY *= -1;
    }
}
```

If you are completely lost with the code, [check this website](https://happycoding.io/tutorials/p5js/animation/bouncing-line), it gives a lengthy explanation about the code.

*Submission*: - (we will discuss the code in class)


## Task 04.02 - Code adjustment

Make at least one adjustment to the code in 4.1. to make it look different 

*Submission*: Add a link to your sketch in your OwnCloud file.

## Task 04.03 - Inspiration

Find one code example that inspires you. You can use, e.g., the collections that are listed in [Script 02 - Setup: Resources and Community](../../02_scripts/ccfb_ss23_02_setup_script.md#resources-and-community). Explain briefly what you like about the example.

*Submission*: Add a link to the example and your explanation as text in your OwnCloud file.


---

*Happy Animating!*
