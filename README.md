# CSS Animations

> CSS animations make it possible to animate web elements with simple CSS style configurations. Like a movies, you need to provide a set of keyframes to indicate the start and end states of the animation styles, as well as the intermediate waypoints.

![CSS Animation demo](https://media.giphy.com/media/3oxRmzoI5NqmzugscE/giphy.gif)
*CSS animations demo*

## Why use CSS over JavaScript for animations?

- It's really simple to make animations! You can apply it without any knowledge of JavaScript.
- They run very well and the rendering engine will keep the performance as smooth as possible.
- It lets the browser control the animation sequence and optimize the performance to improve the efficiency.


## Animation configurations

| **properties** | **description** |
|------------|:------------|
|**animation-delay**| Configures the delay between the time the element is loaded and the beginning of the animation sequence. |
|**animation-direction**|Configures whether or not the animation should alternate direction on each run through the sequence or reset to the start point and repeat itself.|
|**animation-duration**|Configures the length of time that an animation should take to complete one cycle.|
|**animation-iteration-count**|Configures the number of times the animation should repeat; you can specify infinite to repeat the animation indefinitely.|
|**animation-name**|Specifies the name of the @keyframes at-rule describing the animation's keyframes.|
|**animation-play-state**|Lets you pause and resume the animation sequence.|
|**animation-timing-function**|Configures the timing of the animation; that is, how the animation transitions through keyframes, by establishing acceleration curves.|
|**animation-fill-mode**|Configures what values are applied by the animation before and after it is executing.|

**Source:** [MDN CSS animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)

## Getting started

I recommend using the **[stencil](https://github.com/stanleycyang/stencil)** generator to make a basic HTML / CSS / JS boilerplate. 

To install [stencil](https://github.com/stanleycyang/stencil), run the following:

```bash
$ curl https://raw.githubusercontent.com/syang019/stencil/master/stencil -O
$ chmod 755 stencil
$ sudo mv stencil /bin
```

Then create a starter boilerplate, run:

```bash
$ cd ~/Desktop
$ stencil css_animations
```

Your directory structure should look like this:


	├── README.md
	├── css
	│   └── style.css
	├── index.html
	└── js
	    └── main.js

Alternatively, you can also just do the following:

```bash
$ cd ~/Desktop
$ mkdir -p css_animations/css css_animations/js
$ touch css_animations/README.md css_animations/css/style.css css_animations/js/main.js css_animations/index.html
$ cd css_animations
```

## A basic animation

We're going to create a basic example to change the color of a rounded box. 

In your `index.html`

```html
<html>
  <head>
    <!-- Title of our page -->
    <title>CSS animations</title>
    <!-- Soure in stylesheet -->
    <link rel="stylesheet" type="text/css" href="css/style.css">
  </head>
  <body>
    <h1>CSS animations</h1>

    <!-- The div that we will change colors with -->
    <div class="change-color"></div>

    <script src='js/main.js'></script>
  </body>
</html>
```

This is just a basic HTML webpage with a `<html>`, `<head>`, and `<body>` tag. Make sure your `css/style.css` is sourced into the page.

```css
/* Change color class */
.change-color {
  
  /* Describe the width and height of the div */
  width: 100px;
  height: 100px;
  
  /* Red background */
  background-color: red;

  /* Rounded borders */
  border-radius: 5px;

  /* Apply the animation */
  -webkit-animation-name: changeColor; /* Chrome, Safari, Opera */
  -webkit-animation-duration: 4s; /* Chrome, Safari, Opera */
  
  animation-name: changeColor;
  animation-duration: 4s;
}

/* Chrome, Safari, Opera */
@-webkit-keyframes changeColor {
  from {
    background-color: red;
  }
  to {
    background-color: yellow;
  }
}

@keyframes changeColor{
  /* Start from red */
  from {
    background-color: red;
  }
  /* Go to yellow */
  to {
    background-color: yellow;
  }
}
```

We start by defining the default box by providing some basic styles (width, height, background-color, border-radius).

In order to create animations, all we have to do is create an animation code block with the keyword **@keyframes**. In this example, we provided the name **changeColor** to our animation. 

```css
@keyframes changeColor {

}
```

Then we're going to add the starting and ending styles:

```css
@keyframes changeColor{
  /* Start from red */
  from {
    background-color: red;
  }
  /* Go to yellow */
  to {
    background-color: yellow;
  }
}
```

This will change the styles from red to yellow. In order to connect the styles with the element, we have to call it as such:

```css
/* Change color class */
.change-color {
  animation-name: changeColor;
  animation-duration: 4s;
}
```

By adding `animation-duration`, it means that it will change from red to yellow in **4 seconds**.

Did you happen to notice this?

```css
/* Chrome, Safari, Opera */
@-webkit-keyframes changeColor {
  from {
    background-color: red;
  }
  to {
    background-color: yellow;
  }
}
```

This `webkit` portion is what we call the [CSS Vendor Prefixes](http://css-snippets.com/browser-prefix/).

```
-moz-     /* Firefox and other browsers using Mozilla's browser engine */
-webkit-  /* Safari, Chrome and browsers using the Webkit engine */
-o-       /* Opera */
-ms-      /* Internet Explorer (but not always) */ 
```

**Explanation:**

These browser prefixes are needed as the browsers experiment and test out their implementations of the newer CSS3 properties. Sometimes all the prefixes are not always needed, but it usually does not hurt to include them, as long as you make sure to put the non-prefixed version last.

**The results:**

![Colors animation](https://media.giphy.com/media/xT77XVap1Q2oX9Wz8A/giphy.gif)

Our first animation works! Let's build on what we just learned to make more complex animations.

## Using percentages in place of `from` and `to`

Let's change the animation keyframes code to look like this:

```css
@-webkit-keyframes changeColor {
  /* Start from red */
  0%{
    background-color: red;
  }
  25%{
    background-color: yellow;
  }
  50%{
    background-color: purple;
  }
  100%{
    background-color: blue;
  }
}

@keyframes changeColor{
  /* Start from red */
  0%{
    background-color: red;
  }
  25%{
    background-color: yellow;
  }
  50%{
    background-color: purple;
  }
  100%{
    background-color: blue;
  }
}
```

To make our animation continue to run infinitely, we can apply the `animation-iteration-count` to `infinite`:

```css
.change-color {

	... Previous code ...
	
	animation-name: changeColor;
	animation-duration: 4s;
 	animation-iteration-count: infinite; /* Our animation continues infinitely */
}
```

**Result:**

![Infinite animation iteration](https://media.giphy.com/media/3oxRmlruc8swMMvneU/giphy.gif)

> **Note:** You can also apply animation-delay to delay the animation when it loads. Try it out!

## Spinning animation

Let's readjust our code now. Our goal is to create a spinning box with CSS:

**HTML:**

```html
<html>
  <head>
    <!-- Title of our page -->
    <title>CSS animations</title>
    <!-- Soure in stylesheet -->
    <link rel="stylesheet" type="text/css" href="css/style.css">
  </head>
  <body>
    <h1>CSS animations</h1>

    <div class="spin"></div>

  </body>
</html>
```

**CSS:**

```css
.spin {  
  width: 200px;
  height: 200px;
  background-color: yellow;
  animation: spinning 5s infinite;
  -webkit-animation: spinning 5s infinite;
}

@keyframes spinning {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);    
    background-color: red;
  }
}

@-webkit-keyframes spinning {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);    
    background-color: red;
  }
}
```

Notice how this time around, we set the animations all in the same line?

```css
.spin {  
	...
	animation: spinning 5s infinite;
}
```

This is a way we can shorthand our animation code. The structure looks like this:

```
animation: name duration timing-function delay iteration-count direction fill-mode play-state;
```

**Spinning result:**

![Spinning animation](https://media.giphy.com/media/xT77YbRrjgVF8bCKRO/giphy.gif)

## Conclusion

At this point in time, you have the fundamental knowledge to create CSS animations on your own. Go forth and make robust animated websites :-)


## References

- [Translate vs. left / top by Paul Irish](http://www.paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/)
- [MDN CSS Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)