To add an image to the page, we'll want to:

1. Upload the image file to our project.
2. Add an image to our webpage.
3. Get the image for use in JavaScript


## Uploading the File

Note: if you just upload an image to your Vite project, it will seem to work, but when you publish the project, it won't work properly. To work around this, create a folder called `public` at the top level of your project and put images there.

So, for example, I could upload a file called `cat.jpg` to the folder `public`

## Add image to the webpage

Now, we will want to add the image to our webpage. Let's do this just using HTML by editing our HTML directly. Just below the close body tag `</body>` we'll add the following:


*index.html*
```html
  <div style="display:block;">
    <img id="cat" src="/cat.jpg">
  </div>
```

Once you see that your cat is in fact showing up on the page, you can change the style to read `"display:none"` instead of `"display:block"` so the image doesn't show up on your page.

## Getting the image in JavaScript

To get the image element in JavaScript, we'll use `document.querySelector('#cat')` where the `#cat` corresponds to `id=cat` in our HTML.

Let's create a file for our image code:

*cat.ts*
```
import {canvas,ctx} from './canvas';

let imageElement = document.querySelector('#cat');
const width = 150;
const height = 150;
export function drawCat (x, y) {
  ctx.drawImage(imageElement, x, y, width, height);
}
```

A final note: you can check out the [drawImage](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/drawImage) docs for a more complete
explanation of what's possible with that function, but this should get you started :)


[See also my generic JS docs](https://thinkle-iacs.github.io/js1-docs//canvas/images.html)