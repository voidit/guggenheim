# Guggenheim
An algorithm for a perfectly balanced Gallery for Kirby CMS

## Let's kick things off with a demo 😍
**See it live:**

https://sitemarina.github.io/guggenheim/

**Screenshot:**

[![Screenshot of Guggenheim](https://raw.githubusercontent.com/SiteMarina/guggenheim/master/guggenheim/screenshot.jpg)](https://sitemarina.github.io/guggenheim/)

## Idea
Guggenheim is a plugin for [Kirby CMS](http://getkirby.com) which generates beautiful galleries through an algorithm for a perfectly balanced layout, which you might know from [the awesome image grids at medium.com](https://medium.com/the-story/introducing-image-grids-c592e5bc16d8)

Read more into the math and science behind the algorithm here: [The algorithm for a perfectly balanced photo gallery](https://www.crispymtn.com/stories/the-algorithm-for-a-perfectly-balanced-photo-gallery)

In my search for the perfect gallery, which could do this linear partition against the images,
I really wasen't getting excited about all the countless client-side javascript solutions to the problem.
As I care deeply about mobile, i simply didn't wanted to make the devices responsible for this task and wanted a PHP solution for the linear partition.

## Single Domain License
Buy a Single Domain License here https://sitemarina.github.io/guggenheim/ - **I am currently struggling pretty bad 😥**

**Pre-launch Option**
- I'll send you the plugin as a regular ol' .zip file to the email provided at purchase.
- If you for some reason don't like it, send me an email me for an refund.
- I'm working on an easier way to ship updates through Git - I'll send you an email when it's ready.

## Setup
Grab yourself a copy of the most [awesome NoDB file-based CMS ever Kirby](http://getkirby.com)

1. Copy the guggenheim folder into site/plugins
2. Integrate the styles from [guggenheim/guggenheim.css](https://raw.githubusercontent.com/SiteMarina/guggenheim/master/guggenheim/guggenheim.css) into your frontend design or framework
3. Spice it up with [PhotoSwipe (get it here)](https://github.com/dimsemenov/PhotoSwipe) and utilize it by integrating [guggenheim/guggenheim-hearts-photoswipe.js](https://raw.githubusercontent.com/SiteMarina/guggenheim/master/guggenheim/guggenheim-hearts-photoswipe.js) into your frontend design or framework

## Settings
in your site/config/config.php

```php
// Add aditional classes to the guggenheim gallery element
c::set('guggenheim.classes', 'gallery zoom margin-center');

// Guggenheim is meant to be used with PhotoSwipe
// But if you for some reason don't want to use it, you can remove it additionals with
c::set('guggenheim.photoswipe', false);

// Guggenheim uses some basic srcset and sizes for basic responsiveness and highres support
// if you want to disable it, and make your own
c::set('guggenheim.srcset', false);

// Guggenheim adds a kirbytext tag, the default is 'gallery', but you can change it with
c::set('guggenheim.kirbytext.tagname', 'guggenheim');
```

## Usage


### With kirbytext

**Super simplistic -Generate a Guggenheim gallery with all the page images**
```markdown
(gallery:) or (gallery: all)
```

**More generally, you want to pick out the pictures to make the gallery from, you do it like this**
```markdown
Comma separated:
(gallery: image-1.jpg, image-2.jpg, image-3.jpg)

Pipe separated:
(gallery: image-1.jpg | image-2.jpg | image-3.jpg)

..heck even both:
(gallery: image-1.jpg | image-2.jpg, image-3.jpg)
```

**Options**

Guggenheim lets you set some options for each gallery.

- **width** Which is the width of the gallery, all image will be resized through a linear partition to fit this width, and it will also be the max-width of the gallery (to prevent upscaling).
- **height** This is a ideal hight for images to fit too, it'll only be used as a guideline for the linear partition to maximum fit into, it's there for you to play around with for each specifik gallery
- **border** Sets the space between images in pixels

```markdown
(gallery: image-1.jpg, image-2.jpg, image-3.jpg width: 800 height: 350 border: 10)
```

### In your templates
Use the Guggenheim gallery in your templates

```php
$images = $page->images()->sortBy('sort', 'asc');
echo guggenheim($images, array('width' => 800, 'height' => 350, 'border' => 10));
```

## Features
- _Mostly_ perfect balanced gallery generated by a linear partition algorithm server-side, to preventing the usual overhead that JavaScript brings in terms of browser paint, reflows, grid calculations and DOM manipulations.
- If a 'caption' field is present for the image, it'll be added as a visually hidden figcaption, visible when opened in PhotoSwipe.
