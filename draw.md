# Welcome to the Screensaver Project!

To keep our lives simple and organized, let's try to use the following rules for drawings in this project:

1. Every drawing will be a function that takes x and y coordinates as arguments.
2. Every drawing will go in its own module.

## Our First Drawing

I'm going to start by drawing a simple balloon. I encourage you to change the drawing slightly to make it your own.

First, we'll need to create a new file called `balloon.ts` in our folder called `app`:

We'll want to import this file in `index.ts` otherwise it won't run...
*index.ts*
```typescript
import './canvas';
import './balloon';
```

*balloon.ts*
```typescript
import {ctx, canvas} from './canvas';

function drawBalloon (x,y) {
  // Draw a white string
  ctx.beginPath();
  ctx.strokeStyle = 'white';
  ctx.moveTo(x,y+130);
  ctx.lineTo(x,y);
  ctx.stroke();
  // Draw a red circle...
  ctx.beginPath();
  ctx.fillStyle = 'red';
  ctx.arc(x,y,50,0,Math.PI*2);
  ctx.fill();
  // draw a white square on the circle
  // for the "reflection"
  ctx.strokeRect(x+10,y+10,10,10);  
}
```

*At this point, your code won't do anything because you've only defined a function!*

Now make sure to *call* the function, either in balloon.ts at the bottom or in your `index.ts` file. This will let you test out your drawing.

You should be able to call the function multiple times and see multiple balloons show up on screen.

## A note on process

It's good practice to start with something really simple, so here's a good starter template for starting any new drawing you want to add to your project.

### Step 1: Get a small drawing working

First, create a file like this -- this one just draws a tiny square:

*newThingy.ts*
```typescript
import {ctx,canvas} from './canvas';
export function drawThingy (x,y) {
  ctx.strokeRect(x,y,10,10);
}
```

*index.ts*
```typescript
import {drawThingy} from './newThingy';
// Draw two thingies...
drawThingy(50,50);
drawThingy(150,50);
```

### Step 2:
Now that you have two squares showing up on screen, go back and start adding to your drawing until you have something you like.

# Next steps...

Got your drawing already? Awesome! Go you! Now it's time to work on animation!
- [back to instructions](./instructions.md)
- [animation](./animation.md)