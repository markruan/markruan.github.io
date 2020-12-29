---
title: particles.js
categories:
  - study
---
## particles.js学习

  今天突发奇想优化下主题，想起了之前看过炫酷的星云效果，就搜索了下... 

效果见主页

##  Installation

To install particles.js you can [download](https://github.com/marcbruederlin/particles.js/archive/master.zip) the latest version, install it via npm:

```node
npm install particlesjs —-save
```

or use the CDN:

```
https://cdnjs.cloudflare.com/ajax/libs/particlesjs/2.2.2/particles.min.js
```

## Usage

````html
<body>
  …   
<script src=
"path/to/particles.min.js"
></script>
</body>
````

Add a canvas element to your markup (it should be the last element):

```html
<body>
  …
  
<canvas class=
"background"
></canvas>
  
<script src=
"path/to/particles.min.js"
></script>
</body>
```



And Initialize the plugin on DOM ready:

```javascript
window.onload = function() {
    Particles. init
        ({
            selector: 
        '.background'
          });
};
```



## Options

| Option           | Type               | Default | Description                                                  |
| ---------------- | ------------------ | :-----: | ------------------------------------------------------------ |
| selector         | string             |    -    | *Required:* CSS selector of your canvas element              |
| maxParticles     | integer            |   100   | *Optional:* Maximum amount of particles                      |
| sizeVariations   | integer            |    3    | *Optional:* Amount of size variations                        |
| speed            | integer            |   0.5   | *Optional:* Movement speed of the particles                  |
| color            | string or string[] | #000000 | *Optional:* Color(s) of the particles and connecting lines   |
| minDistance      | integer            |   120   | *Optional:* Distance in px for connecting lines              |
| connectParticles | boolean            |  false  | *Optional:* true/false if connecting lines should be drawn   |
| responsive       | array              |  null   | *Optional:* Array of objects containing breakpoints and options |

### Responsive option

With the responsive option, you can add or override options for different screen sizes:

````json
Particles. init ({ 
  // normal options
  selector: '.background',
  maxParticles:450,
  
// options for breakpoints
  responsive: [
    {
      breakpoint: 768,
      options: {
        maxParticles: 200,
        color: '#48F2E3',
        connectParticles:false
      }
    }, {
      breakpoint:425,
      options: {
        maxParticles: 100,
        connectParticles: true
      }
    }, {
      breakpoint: 320,
      options: {
        maxParticles:  0 // disables particles.js
      }
    }
  ]
});
````



## Methods

| Method          | Description                         |
| --------------- | ----------------------------------- |
| pauseAnimation  | Pauses/stops the particle animation |
| resumeAnimation | Continues the particle animation    |



### Use the public methods

 

 

 ````json
var particles = Particles.init({
// options
});
// E.g. gets called on a button click
function pause () {
  particles. pauseAnimation ();
}
// E.g. gets called on a button click
function resume () {
  particles. resumeAnimation ();
}
 ````

