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

A basic for loop has three components:
1. You create a counting variable
2. You tell the loop at what point to stop running.
3. You add to the counting variable.

A for loop that just counted from 1 to 10 would look like this:
```typescript
for (let i=1; i<=10; i += 1) {
  console.log('The count is ',i);
}
```

For my drawing, I'm going to count by steps of 15 pixels
so there is a 15 pixel gap between each line I make in my curve:

```typescript
export function drawDesign (x, y, step, size) {  
  // Move the variable i up by 15 each time
  // Creating a "curve" made up of straight lines
  for (let i=0; i<step; i += 15) {
    ctx.strokeStyle = 'white';
    ctx.beginPath();
    // We move over on the X axis
    ctx.moveTo(
      x + i,
      y
    );
    // We move up on the Y axis...
    ctx.lineTo(
      x,y+size-i
    )
    // draw the line
    ctx.stroke();    
  }
}
```

This should now create a pretty design with a for loop.

### WARNING!

When JavaScript is running in your browser, nothing else can run. For this reason, the only loops I recommend for my beginning students are *for* loops, which have a built in "end" condition. Your computer can do thousands of calculations very quickly, but be careful not to accidentally make a loop that will never end or you'll crash your browser :)

## Using the modulo to alternate through options...

Let's say I want to alternate colors for my lines.

The first step is to define a list of colors I'll use. This will be
your first list! Lists are created in JavaScript with the characters `[` to start the list and `]` to end it and a `,` between each value.

```typescript
let colors = ['pink','green','yellow','white'];
```

Now, if we want to move through those colors in order,
we can do so by setting a variable to count each line we draw and 
then using that variable to access the corresponding color (so the first line gets the first color, the second the second color and so on).

```javascript
let lineCount = 0
```

We can then get a color by using *index notation* to get the corresponding item from a list. Note, the first item of a list 
is item "0" and not item "1" (sorry, I don't make the rules -- but this 
is the way in pretty much every programming language so get used to it!)
```javascript
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

To fix that, we will need to use modulo operator. Modulo gives you the remainder when dividing by a number. So, for example, 4 modulo 2 is 0 (because 4 divided by 2 is 2 exactly), but 5 modulo 2 is 1 (because 5 divided by 2 is 2 remainder 1). The remainder is a very handy thing to use when we want to cycle in programming, since you can use remainders to go from a count to an alternating pattern.

One last thing to know about a list is it has a property `length` which tells you how many items it has. Given all that, here's the revision we need to make of the code above to get alternating line colors working:

```typescript

ctx.strokeStyle = colors[lineCount % colors.length];
lineCount += 1;
```