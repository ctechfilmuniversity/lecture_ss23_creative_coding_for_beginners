---
layout: default
title: Exercise 02
parent: Exercises
nav_order: 1
---

# Creative Coding For Beginners
  
Prof. Dr. Lena Gieseke \| l.gieseke@filmuniversitaet.de  
  
  
# Exercise 02 - Program Flow & Interaction

This session is due on **Monday, May 15th**.  

* [Creative Coding For Beginners](#creative-coding-for-beginners)
* [Exercise 02 - Program Flow \& Interaction](#exercise-02---program-flow--interaction)
    * [Task 02.01 - Scripts](#task-0201---scripts)
    * [Task 02.02 - Program Layout](#task-0202---program-layout)
    * [Task 02.03 - Errors](#task-0203---errors)
    * [Task 02.03 - Interaction](#task-0203---interaction)


## Task 02.01 - Scripts

Recap the scripts:

* [Program Flow and Interaction](../../02_scripts/ccfb_ss23_04_flow_script.md)
* [Color Systems](../../02_scripts/ccfb_ss23_05_colorsystems_script.md)

*Submission*: -

## Task 02.02 - Program Layout

This code executes just fine however its layout is unacceptable. Copy the following code and layout it properly. Can you understand what it does?

```js
function setup() 

{createCanvas(windowWidth, windowHeight);background(255);noStroke();noLoop();}function 

draw() {}
function keyPressed() {fill(random(255), random(255), random(255));ellipse(random(windowWidth), random(windowHeight), random(200));}
```

*Submission*: Add a link to your sketch in your OwnCloud file.

## Task 02.03 - Errors

This code has three errors. Can you find and fix them? Make sure to read the error messages, they might (or might not) help you find the issues.

```js
function setup() {
    createCanvas(500, 500); 
    background(30, 230, 230);
    
    stroke(0, 0, 0);
    strokeWeight();
}

function draw() 

    // Nose
    fill(255, 255, 0);
    ellipse(250, 250, 150, 200);
    
    // Eye L
    fill(0, 255, 0);
    ellipse(150, 130, 50, 50);

    // Eye R
    ellipse(350, 130 50, 50);
    
    noFill();
    arc(250, 350, 200, 150, radians(-10), radians(180));	
}
```

*Submission*: Add a link to your sketch in your OwnCloud file.


## Task 02.03 - Interaction

Create a sketch up to your liking and that uses interaction and / or [animation](https://editor.p5js.org/legie/sketches/ZGkf_1vzt). The sketch does not need to be particularly creative or beautiful. The goal is to practice the learned functionalities.

  

*Submission*: Add a link to your sketch in your OwnCloud file.

---

*Happy Flowing!*

