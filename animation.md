# Animation!

Before you can animate, you're going to need to have a drawing working and you're going to need to have a drawing that can *move* in response to a parameter changing.

## Are you ready?

So, ideally, you have a function like `drawBalloon` and if you call `drawBalloon(10,10)` you'll get a balloon in the top left corner and if you then call `drawBalloon(50,50)`, the balloon will move down and to the right.

If you don't have that working yet, go back to the [drawing](draw.md) step or ask for help!

## Onward!

The basic concept of animation is simple: draw something on the canvas, then erase the screen, then draw it again!

Because erasing makes debugging hard, we'll start by just drawing, and then we'll add in the erasing.

Our animate code will need to import whatever drawing code we wrote last time in the [drawing](draw.md) step.

**animate.ts**
```typescript
import {ctx, canvas} from './canvas';
import {drawBalloon} from './balloon';

let x = 10;
let y = 10;

function animate (ts) {
  drawBalloon(x,y);
  x += 1;
  y += 1;
  // run ourselves again after 1 "tick"
  // (about 1/60th of a second)
  window.requestAnimationFrame(animate);
}

window.requestAnimationFrame(animate)
```

If this code works correctly, you should see a balloon blurring across the screen.

In order to make it animate, you just need to add a step where you erase the screen before drawing, like this:

```typescript
function animate (ts) {
  // erase the whole screen
  ctx.clearRect(0,0,canvas.width,canvas.height);
  // draw the balloon
  drawBalloon(x,y);
  // Add one to x and y...
  x += 1;
  y += 1;
  // run ourselves again after 1 "tick"
  // (about 1/60th of a second)
  window.requestAnimationFrame(animate);
}
```

## Where'd my balloon go?

### First, let's break this problem down!
You'll notice that in this code, the balloon disappears and never comes back. In practice, your code is going to get more complicated quickly, so I would recommend taking the simple lines:

```typescript
x += 1;
y += 1;
```

And moving them into their own function, where it can grow more complex.

Your first step would look like this:
```typescript
function animate (ts) {
  // erase the whole screen
  ctx.clearRect(0,0,canvas.width,canvas.height);
  // draw the balloon
  drawBalloon(x,y);
  // Add one to x and y...
  updatePosition();
  // run ourselves again after 1 "tick"
  // (about 1/60th of a second)
  window.requestAnimationFrame(animate);
}

function updatePosition () {
  x = x + 1;
  y = y - 1;
}
```

At this point, all you've done is moved code around: everything should still run exactly the same (make sure it does!).

### Making a fancier "udpate" function

We'll want to add some if statements to check if our x or y values are too big or too small. Since our balloon currently only moves in one direction, we only have to worry about movement in one direction for now, but you will likely need to write more if statements later on.

```typescript
function updatePosition () {
  x = x + 1;
  y = y - 1;
  // If we go off the right, come back
  // around the left
  if (x > canvas.width) {
    x = 0;
  }
  // if we go off the top, come back at the
  // bottom
  if (y < 0) {
    y = canvas.height;
  }
}
```

[A much fancier balloon example](fancyBalloon.md)




## Some technical notes on requestAnimationFrame

A few notes about animation: we ask the browser window to run animate as often as possible, but the computer is smart enough to save resources by not running the code if you, for example, switch to another tab to watch a YouTube video. 

Every time you call animate, the browser will give you a timestamp, which is a number representing the current time. You can store the value of the timestamp and then calculate how long it has been since your last run to run your animation at a smooth speed regardless of computer speed.
