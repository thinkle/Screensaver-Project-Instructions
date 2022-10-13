# Rotating the Canvas

The drawing context provides a simple rotate function (`ctx.rotate`), but it's a little tricky to use.

The way rotating works in JavaScript is that you actually rotate the entire drawing context -- think of it as rotating the whole sheet of paper. Therefore, if you call `ctx.rotate(Math.PI/2)` (that should rotate the canvas 45 degrees) and then draw a line, the line will not only rotate but also move (imagine you're holding the canvas down by the top left corner and moving it -- that's what rotate does)

## Moving *and* rotating the canvas

Luckily, there's a command to *move* the whole canvas, and then rotate it. If we do this, we will effectively rotate our drawing around any point we choose. So lets say I want to draw a rectangle centered around the point 40,40 and then rotate it. The first step is I will need to actually draw the rectangle in the top left corner, like this:

```typescript
// 20 pixel rectangle centered on 0,0
ctx.strokeRect(-10,-10,20,20); 
```

Next, we can use translate to move that drawing
back to 40,40

```typescript
ctx.translate(40,40);
ctx.strokeRect(-10,-10,20,20); 
```

Final step is to rotate in addition to translating, like this:

```typescript
ctx.translate(40,40);
ctx.rotate(Math.PI/4); // 45 degrees
ctx.strokeRect(-10,-10,20,20); 
```

A final final step is we should put the canvas
back to normal when we're done, with `ctx.resetTransform()`

```typescript
ctx.translate(40,40);
ctx.rotate(Math.PI/4); // 45 degrees
// Now do our drawing...
ctx.strokeRect(-10,-10,20,20); 
// Now we reset the transform
// so future drawings will be as we
// expect them
ctx.resetTransform()
```

## Creating a "drawRotated" function

Imagine you want to build an animation with many items, all of which rotate -- maybe a rotating ball of yarn moves by a floating cat, which itself can turn.

We could just copy paste the lines of code above everywhere we need rotation, or we could make a convenience function to do it for us:

```typescript
function drawThingRotated (...) {
  ctx.translate(x,y);
  ctx.rotate(Math.PI/4); // 45 degrees
  // Now do our drawing...
  DO A BUNCH OF STEPS NOW TO
  DRAW WHATEVER WE WANT HERE AT 0,0
  // Now we reset the transform
  // so future drawings will be as we
  // expect them
  ctx.resetTransform()
}
```

But how do we insert the draw-whatever step
in the *middle* of our function?

Luckily, we already have a concept for doing
a bunch of steps: the *function*. So in this case
what we need to do is have our function accept a 
function as an argument, like so:

```typescript
function drawThingRotated (drawingFunction, 
                          x, y, angle) {
  ctx.translate(x,y);
  ctx.rotate(angle); // 45 degrees
  // Now do our drawing...
  drawingFunction(0,0); 
  // Now we reset the transform
  // so future drawings will be as we
  // expect them
  ctx.resetTransform()
}
```

In my example above I assumed the drawing function took x and y parameters, but of course that depends on the design of your program. The key thing to understand is that whatever function you *hand* to drawThingRotated will be called *after* the translate and rotate section.

If you would rather hand your function the angle in degrees than radians, you can modify our rotate line to do the conversion, like this...

```typescript
ctx.rotate(angle * 180 / Math.PI);
```