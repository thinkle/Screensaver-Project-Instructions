## Making Our Balloon Fancy

This tutorial assumes you've gotten a working [animation](animation.md) and you're looking for an example of more complicated motion.

We will focus our efforts on the `updatePosition` function, which knows about our balloon motion so far.

We can think of the balloons motion in two different ways: up and down and left to right.

For the up motion, let's just keep the balloon floating steadily up. For the left-to-right motion, though, we could introduce a little randomness into the equation.

### Random values

In JavaScript, the function
```javascript
Math.random()
```
gives you a random number between 0 and 1.

We can then multiply by that number to create any motion we want. [Here's a quick demonstration I threw together of how scaling random numbers works](https://codepen.io/thinkle-iacs/pen/eYrjoYx)

So if we want our balloon to flit to the left and right, we can just add a random value to our x value, like so:

```typescript
function updatePosition () {
  x = x + Math.random()*2 - 1;
  y = y - 1;
  ...
}
```

### Many balloons?

That's pretty good, but what if we wanted to make multiple balloons? At that point, we'd suddenly need more than just one x and y value; we'd need many such values for many such balloons.

In this case, it is time to make our first object. An object is just a way to combine a bunch of properties together.

```
function Balloon () {
  this.x = 100,
  this.y = 100,
  this.move = function () {
    this.x += Math.random() * 2 - 1;
    this.y -= 1;
    if (this.y < 0) {
      this.y = canvas.height
    }
  }
}
```
