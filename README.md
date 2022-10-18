# README #

### Link to the project ###
* https://franciscojaviersc.github.io/Responsive-Images/ 

What is to make an image responisve? 
A method for providing the browser with multiple image sources depending on display density, size of the image element in the page, or any number of other factors.

### What is this repository for? ###

* Quick summary: 
This repository is for investigating and trying methods to make responsive images 


### Research ###
* First step,understanding your use case:
  -Resolution Switching: providing different sizes of an image wihtout modifying the content or aspect ratio
  -Art Direction: there is a need to make changes to content or aspect ratio based on the size of the image in the page

* Scenarios where the <img> element can be enought:
  -A fixed width, single density web page
  -Small differences in file size
  -Using vector-based images like SVG


* Srcset Display Density:
We use srcset when we are in a resolution switching use case because it give the browser choice and it can make decisions based pm factors as network conditions or user preference.
```html
Syntax: <img src="cat.jpg" alt="cat" srcset="cat.jpg, cat-2X.jpg 2x">
```
The value of the attribute srcset contains a comma-separated list. Each item in the list contains the path to an image and the density of that image provided as "1x,2x,3x ..."

This solution is recomended for fixed width images but not sufficient for flexible images, in here we might to use srcset's width descriptors.


* Width Descriptors:
The syntax is similar to display desity descriptors, in this case we point the width of the image source, and the browser pics the best source.
Syntax: 
```html
<img src="cat.jpg" alt="cat" srcset="cat-160.jpg 160w, cat-360.jpg 360w">
```
The fact in here is that knowing the size of the viewport, that is what the browser uses to render the image, the browser doesn't have enough information to select the right image source, and here it comes the sizes attribute.


* Sizes Atributte:

Sizesis required when you are using srcset width descriptors, but it only makes sense if you are using the width descriptors, if ypu are using display density descriptors, you don't need the sizes attribute.

Specifying the sizes we are telling the browser what size the image will be in relation to the size of the viewport, and we can tell the browser how that relationship changes as the size of the viewport changes.

Syntax:
```html
<img src="cat.jpg" alt="cat"
  srcset="cat-160.jpg 160w, cat-320.jpg 320w, cat-640.jpg 640w, cat-1280.jpg 1280w" 
  sizes="(max-width: 480px) 100vw, (max-width: 900px) 33vw, 254px">
```
This work like, if the view port is 480 pixels wide or smaller the image will be the 100% of the viewport width

* Picture Element (Art direction use case):
The <picture> element contains a series of <source> child elements and at the end an <img> element that is required

Syntax: 
```html
<picture>
  <source media="(min-width: 900px)" srcset="cat-vertical.jpg">
  <source media="(min-width: 750px)" srcset="cat-horizontal.jpg">
  <img src="cat.jpg" alt="cat">
</picture>
```
The value of the media attribute is a madeia query the first source whose media query matches is the one that is used, if no one match the <img> element is used

* Type Attribute:
This attribute can be added to <source> elemetns inside a <picture> element and allows to declare different image types that the browser can choose from

Syntax:
```html
<picture>
  <source type="image/svg+xml" srcset="logo.xml">
  <source type="image/webp" srcset="logo.webp"> 
  <img src="logo.png" alt="ACME Corp">
</picture>
```
