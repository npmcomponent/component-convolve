*This repository is a mirror of the [component](http://component.io) module [component/convolve](http://github.com/component/convolve). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/component-convolve`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*

# convolve

  Canvas [convolution](http://en.wikipedia.org/wiki/Convolution) filter.

  ![](maru_edges.jpg)

## API

### convolve(matrix)

  Return a new convolution `Filter` with the given `matrix`.

### Filter#factor(n)

  Change the factor to `n`, defaults to `1`.

### Filter#bias(n)

  Change the bias to `n`, defaults to `0`.

### Filter#width(n)

  Canvas width.

### Filter#height(n)

  Canvas height.

### Filter#apply(input, result)

  Apply the convolution filter to the `input` ImageData, populating 
  the `result` ImageData. This is a lower-level method, you most
  likely want to apply to the entire canvas, in which case use below:

### Filter#canvas(canvas)

  Apply the convolution filter to the entire `canvas`
  and immediately draw the results.

## Example

```js
var convolve = require('convolve');
var canvas = document.querySelector('canvas');
var ctx = canvas.getContext('2d');

var img = new Image;
img.onload = draw;
img.src = 'maru.jpg';

var sharpen = [
  [-1, -1, -1],
  [-1, 9, -1],
  [-1, -1, -1]
];

var blur = [
  [0, .2, 0],
  [.2, .2, .2],
  [0, .2, 0],
];

// factor 1 / 7
var motionBlur = [
  [1, 0, 0, 0, 0, 0, 0],
  [0, 1, 0, 0, 0, 0, 0],
  [0, 0, 1, 0, 0, 0, 0],
  [0, 0, 0, 1, 0, 0, 0],
  [0, 0, 0, 0, 1, 0, 0],
  [0, 0, 0, 0, 0, 1, 0],
  [0, 0, 0, 0, 0, 0, 1]
];

var edges = [
  [0, -1, 0],
  [-1, 4, -1],
  [0, -1, 0]
];

function draw() {
  canvas.width = img.width;
  canvas.height = img.height;
  ctx.drawImage(img, 0, 0);
  convolve(motionBlur)
    .factor(1 / 7)
    .canvas(canvas);
}
```

# License

  MIT

