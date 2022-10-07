# Instructions  
Your first step will be setting up the project itself so you can see and draw on a canvas. 

## About this project
When you open this project, there is a bare-bones `index.html` file which imports `main.js`.  `main.js` in turn imports `app/index.ts` which is where you should put an index of all the files you create.

To keep your code easy to read, we're going to use *modules* for this project, so each new step will involve creating a new module.

## Setup our Canvas

Our first module will give us a canvas object. Let's go ahead and create a new file in the `app/` folder to put our canvas creating code in.

We will then want to import that file in `index.ts`

*index.ts*
```typescript
import "./canvas";
```
*canvas.ts*

```typescript
export let canvas = document.createElement('canvas');
export let ctx = canvas.getContext('2d');
// dark blue background
canvas.style.backgroundColor = '#222242';


document.querySelector('#app')
  .appendChild(canvas);
```

## Next Steps...

At this point, you have a canvas with a dark blue background. Your canvas will be the default size, which is 300x150 pixels.

### Customize the size

You can use JavaScript to make the canvas any size you want, by changing its width and height properties, like this:

```typescript
canvas.width = 500;
canvas.height = 800;
```

At this point, you should have a basic canvas ready to roll. You can customize the size and color to your liking, or you can read on to have some fancier options, like making a full-screen canvas or having one that resizes when the window changes size.

[Back to instructions](instructions.md)

### Getting Fancy

If you want to resize the canvas to fill your screen, you might consider using the `innerWidth` and `innerHeight` properties of the window object, like this:

```typescript
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
```

Or, if you don't like it being quite so big, you could make it a proportion of the window width and height by multiplying by a decimal, like this:

```typescript
canvas.width = window.innerWidth * 0.8;
canvas.height = window.innerHeight * 0.8;
```

### Getting Fancy: Resize?

There is an event you can listen for when the user resizes the browser window. If you put your sizing code in a function, you can attach that code to an event on the window, like this:

```typescript
function resizeCanvas () {
  canvas.width = window.innerWidth * 0.8;
  canvas.height = window.innerHeight * 0.8;
}
window.addEventListener(
  'resize',
  resizeCanvas
);
```

You will of course also want to call your function once when you first load to size it appropriately to whatever the webpage is when it first loads by adding to the bottom of the `canvas.ts` file:

```typescript
resizeCanvas()
```

Note: when you change the canvas size, it will erase all the drawings. If you are creating an animation, this won't be an issue since you're redrawing the canvas 60 times a second, but for other uses it means you might not want to change the canvas size when you resize the browser.

Next step: [drawing](draw.md)

[Back](index.md)