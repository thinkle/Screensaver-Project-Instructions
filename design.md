# Designs!

We don't just have to draw simple items, we can also make patterns and designs. I'm going to show you how to make a simple design out of lines (this is one I love to doodle).

## Getting Started...
Let's start with a file

*design.ts*
```typescript
import {ctx} from './canvas';
export let function drawDesign (x, y, step, size) {
  // Before we draw the full design, let's make
  // sure we get a single line showing up...
  ctx.strokeStyle = 'white';
  ctx.moveTo(x,y);
  ctx.lineTo(x+size,y+size);
  ctx.stroke();
}

drawDesign(10,10,50,200);
```

At this point, your "design" is just a single line.
Make sure this line shows up before moving forward!

## Using a for loop!
Our next step will be to use a for loop to allow us
to run our code multiple times.

```typescript
export function drawDesign (x, y, step, size) {  
  // Move the variable i up by 15 each time
  for (let i=0; i<step; i += 15) {
    ctx.strokeStyle = 'white';
    ctx.beginPath();
    ctx.moveTo(
      x + i,
      y
    );
    ctx.lineTo(
      x,y+size-i
    )
    ctx.stroke();    
  }
}
```

This should now create a pretty design with a for loop.

## Using the modulo to alternate through options...

Let's define a list of colors for our design. This will be
your first list!

```typescript
let colors = ['pink','green','yellow','white'];
```

Now, if we want to move through those colors in order,
we can do so by setting a variable to count each line we draw, like this:

```
let lineCount = 0
```

We can then get a color like this:
```
ctx.strokeStyle = colors[lineCount];
```

That will make the color equal to `"pink"` (the first color in the list).

If we add some code to our loop to change colors, we can *almost* get it working, like this:

```typescript
// Not quite working...
export function drawDesign (x, y, step, size) {  
  let lineCount = 0;
  for (let i=0; i<step; i += 15) {
    
    ctx.strokeStyle = colors[lineCount];
    lineCount += 1;
    ctx.beginPath();
    ctx.moveTo(
      x + i,
      y
    );
    ctx.lineTo(
      x,y+size-i
    )
    ctx.stroke();    
  }
}
```

You'll notice this only works for the first three colors, because once lineCount is bigger than our list of colors, there is no color that corresponds.

To fix that, we will need to use modulo operator, which is the percent symbol. Modulo gives you the remainder when dividing by a number. So, for example, 4 modulo 2 is 0 (because 4 divided by 2 is 2 exactly), but 5 modulo 2 is 1 (because 5 divided by 2 is 2 remainder 1). The remainder is a very handy thing to use when we want to cycle in programming, since you can use remainders to go from a count to an alternating pattern.

One last thing to know about a list is it has a property `length` which tells you how many items it has. Given all that, here's the revision we need to make of the code above to get alternating line colors working:

```typescript

ctx.strokeStyle = colors[lineCount % colors.length];
lineCount += 1;
```