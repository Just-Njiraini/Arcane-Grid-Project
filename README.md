# Building an Arcane-Inspired Image Gallery Using CSS Grid

## Project Overview

This project is an image gallery inspired by the animated series Arcane. It uses CSS Grid to arrange character images into a structured layout, with a full-screen background video to create atmosphere.

The main objective was to practise CSS Grid while exploring how different CSS properties work together to create a responsive and visually appealing webpage.

### Technologies used
- HTML5
- CSS3
- CSS Grid
- CSS positioning
- CSS pseudo-elements
- HTML video element

---

# PART 1: Understanding the HTML

HTML provides the structure of the webpage. In this project, it defines the background video, the main grid container and the individual images.

## 1. The HTML document declaration

```html
<!DOCTYPE html>
<html lang="en">
```

- `<!DOCTYPE html>` tells the browser that this document uses HTML5.
- `<html lang="en">` is the root element of the document. The `lang` attribute identifies English as the primary language, which helps browsers, search engines and assistive technologies.

## 2. The head section

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>
```

**`<head>`**

Contains information about the webpage that is not displayed as its main content.

**`<meta charset="UTF-8">`**

Defines the character encoding. UTF-8 supports a wide range of characters and symbols.

**`<meta name="viewport" content="width=device-width, initial-scale=1.0">`**

This is important for responsive web design.

- `width=device-width` makes the webpage use the actual width of the device.
- `initial-scale=1.0` sets the initial zoom level to 100%.

Without this declaration, mobile browsers may render a webpage as though it were designed for a wider desktop screen.

**`<title>Document</title>`**

Defines the webpage title displayed in the browser tab. For the published project, a more descriptive title would be appropriate.

**`<link rel="stylesheet" href="style.css">`**

Connects the HTML document to the external CSS file.

- `rel="stylesheet"` identifies the linked resource as a stylesheet.
- `href="style.css"` specifies the location of the CSS file.

This separation allows HTML to handle structure while CSS handles presentation.

## 3. The body and main wrapper

```html
<body>
    <div class="page">
```

`<body>` contains the visible content of the webpage.

The `.page` div acts as the main wrapper for the project. It contains both the background video and the image gallery.

This wrapper becomes particularly important when positioning the video behind the gallery.

## 4. Adding the background video

```html
<video class="background-video" autoplay muted loop playsinline>

    <source src="./media/4K.mp4" type="video/mp4">

</video>
```

The HTML `<video>` element allows us to embed a video directly into the webpage.

Let's examine its attributes.

**`class="background-video"`**

Assigns a CSS class that allows us to style and position the video.

**`autoplay`**

Instructs the browser to start playing the video automatically.

**`muted`**

Mutes the video. This is particularly useful because browsers generally restrict autoplay of videos that contain sound.

**`loop`**

Automatically restarts the video when it reaches the end.

**`playsinline`**

Allows the video to play within the webpage on supported mobile browsers instead of automatically switching to fullscreen playback.

**The source element:**

```html
<source src="./media/4K.mp4" type="video/mp4">
```

- `src` specifies the location of the video file.
- `./media/4K.mp4` means the video is stored in a folder named `media`, relative to the HTML file.
- `type="video/mp4"` tells the browser the media format.

The video is placed inside `.page` so that CSS can position it as the background of that section.

## 5. Creating the CSS Grid container

```html
<section class="scene container">
```

This is the main image gallery.

The section has two classes:

- `scene`
- `container`

Both classes are applied to the same HTML element. This allows the element to inherit styling from either CSS class.

In the current stylesheet, `.container` contains the Grid properties that control the gallery layout.

## 6. Creating the individual grid items

The first image:

```html
<div class="layer one">
    <img
        class="cover-image"
        src="./media/arcane.jpg"
        alt=""
    />
</div>
```

Each image is wrapped inside a `<div>`.

**`class="layer one"`**

The element receives two classes:

- `layer` provides shared styling for all grid items.
- `one` provides individual positioning and ordering instructions.

**`<img>`**

Embeds an image into the grid item.

**`class="cover-image"`**

Applies shared image styling, including width, height, opacity and image fitting.

**`src="./media/arcane.jpg"`**

Specifies the image file location.

**`alt=""`**

An empty alternative text indicates that the image is decorative and can be skipped by screen readers. If an image communicates important information, descriptive alternative text should be provided instead.

The same structure is repeated for the remaining images:

- `layer two`
- `layer three`
- `layer seven`
- `layer eight`
- `layer nine`

Each image shares the same `.layer` and `.cover-image` styling but can receive different Grid positioning through its individual class.

## 7. Closing the HTML elements

```html
</section>
</div>
</body>
</html>
```

These closing tags complete the structure:

- `</section>` closes the image gallery.
- `</div>` closes the main page wrapper.
- `</body>` closes the visible document content.
- `</html>` closes the entire HTML document.

---

# PART 2: Understanding the CSS

CSS controls how the HTML elements appear and how they interact with one another.

This project uses CSS Grid as the primary layout system.

## 1. Creating the grid

```css
.container {
    display: grid;
    grid-template-columns: repeat(5, minmax(0, 1fr));
    grid-template-rows: repeat(2, minmax(0, 1fr));
    width: min(800px, 90vw, 160vh);
    height: min(450px, 80vh);
    background-color: transparent;
    gap: 5px;
    aspect-ratio: 5 / 2;
    position: relative;
    z-index: 1;
}
```

Let's break this down.

**`display: grid;`**

This establishes a CSS Grid formatting context.

The element becomes a grid container, and its direct children become grid items.

In this project, the six image wrappers become the grid items.

**`grid-template-columns: repeat(5, minmax(0, 1fr));`**

This creates five columns.

The `repeat()` function avoids having to write the same column definition five times.

Instead of:

```css
grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
```

We use:

```css
grid-template-columns: repeat(5, minmax(0, 1fr));
```

Breaking down `minmax(0, 1fr)`:

- `minmax()` defines a minimum and maximum size for a grid track.
- `0` allows the track to shrink to zero if necessary.
- `1fr` allows it to receive one equal fraction of the available space.

Using `minmax(0, 1fr)` helps prevent the intrinsic minimum size of content from forcing grid columns to become wider than intended.

**`grid-template-rows: repeat(2, minmax(0, 1fr));`**

Creates two equally sized rows.

The same `repeat()` and `minmax()` concepts apply here, except they control the height of the grid tracks.

Our basic grid therefore has five columns and two rows.

**`width: min(800px, 90vw, 160vh);`**

Controls the width of the grid.

The CSS `min()` function selects the smallest value among the supplied options.

- `800px` establishes a maximum preferred width.
- `90vw` represents 90% of the viewport width.
- `160vh` represents 160% of the viewport height, expressed as a width constraint.

The browser selects whichever value is smallest.

This helps the grid adapt to different screen dimensions.

**`height: min(450px, 80vh);`**

Controls the grid height.

- `450px` is the maximum preferred height.
- `80vh` represents 80% of the viewport height.

This helps prevent the grid from occupying the entire screen vertically.

**`background-color: none;`**

This declaration was included in my original stylesheet. However, `none` is not a valid value for `background-color`.

If the intention is to have no coloured background, use:

```css
background-color: transparent;
```

**`gap: 5px;`**

Creates a 5-pixel gap between grid rows and columns.

Instead of setting separate margins on every image, Grid's `gap` property handles the spacing.

**`aspect-ratio: 5 / 2;`**

Defines the preferred width-to-height ratio of the grid.

A ratio of 5:2 means that for every five units of width, the preferred height is two units.

This helps maintain the intended proportions when dimensions are not otherwise constrained.

One important detail: because this project explicitly specifies both `width` and `height`, those dimensions take precedence over the preferred aspect ratio.

**`position: relative;`**

Establishes the grid container as a positioning reference for any absolutely positioned descendants.

It also allows the element to participate in a positioned stacking context when combined with a non-auto `z-index`.

**`z-index: 1;`**

Controls the stacking order.

The grid is assigned a higher stacking level than the background video, allowing the images to appear above it.

## 2. Positioning and centring the page

```css
.page {
    min-height: 100vh;
    display: grid;
    place-items: center;
    overflow: hidden;
    position: relative;
}
```

**`min-height: 100vh;`**

Makes the page at least as tall as the viewport.

`vh` stands for viewport height.

`100vh` represents 100% of the viewport height.

**`display: grid;`**

Turns `.page` into another Grid container.

This is an important concept in this project: CSS Grid is being used at two different levels.

- The outer grid centres the gallery.
- The inner grid arranges the images.

**`place-items: center;`**

Centres the gallery horizontally and vertically within the available space.

This shorthand combines:

```css
align-items: center;
justify-items: center;
```

**`overflow: hidden;`**

Hides content that extends beyond the boundaries of the page.

This is useful when working with a full-screen video background.

**`position: relative;`**

Establishes `.page` as the positioning reference for the absolutely positioned background video and overlay.

## 3. Creating a dark overlay using a pseudo-element

```css
.page::before {
    content: "";
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.45);
    z-index: 1;
    pointer-events: none;
}
```

This section introduces CSS pseudo-elements.

A pseudo-element allows us to create and style an element through CSS without adding another HTML element.

**`.page::before`**

Creates a pseudo-element that is rendered before the actual content of `.page`.

**`content: "";`**

Required to generate the pseudo-element.

An empty string creates the element without inserting visible text.

**`position: absolute;`**

Removes the pseudo-element from the normal document flow and allows us to position it relative to `.page`.

**`inset: 0;`**

A shorthand for setting all four positioning offsets to zero:

```css
top: 0;
right: 0;
bottom: 0;
left: 0;
```

This makes the overlay cover the entire page.

**`background: rgba(0, 0, 0, 0.45);`**

Adds a semi-transparent black background.

The `rgba()` function accepts:

- Red: `0`
- Green: `0`
- Blue: `0`
- Alpha: `0.45`

The alpha value controls transparency.

Here, the overlay is 45% opaque, darkening the video while allowing it to remain visible.

**`z-index: 1;`**

Places the overlay above the video.

The gallery also has `z-index: 1`. Since the pseudo-element is generated before the gallery in the page's painting order, the gallery is painted above it.

**`pointer-events: none;`**

Prevents the overlay from intercepting mouse interactions.

This means it does not interfere with interactions with elements underneath it.

## 4. Controlling individual grid items

```css
.layer {
    min-width: 0;
    min-height: 0;
    overflow: hidden;
}
```

These rules apply to every image wrapper.

**`min-width: 0;`**

Allows the grid item to shrink below its intrinsic minimum width.

This is particularly useful when images have large original dimensions.

**`min-height: 0;`**

Allows the grid item to shrink below its intrinsic minimum height.

**`overflow: hidden;`**

Hides any content that extends beyond the grid item's boundaries.

Together, these properties help images remain contained within their allocated grid areas.

## 5. Positioning the background video

```css
.background-video {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: 0;
}
```

**`position: absolute;`**

Removes the video from the normal document flow.

This allows it to sit behind the gallery without occupying a grid cell.

**`inset: 0;`**

Positions the video against all four edges of its containing block, which is `.page`.

**`width: 100%;`**

Makes the video occupy the full width of its containing block.

**`height: 100%;`**

Makes it occupy the full height of its containing block.

**`object-fit: cover;`**

Ensures the video fills its container without distorting its proportions.

If the video and viewport have different aspect ratios, some parts of the video may be cropped.

**`z-index: 0;`**

Places the video behind the overlay and the gallery.

## 6. Fitting and styling the images

```css
.cover-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    opacity: 0.9;
    transition: opacity 0.4s ease;
    filter: brightness(0.85) saturate(0.85);
}
```

This class controls how each image appears inside its grid area.

**`width: 100%;`**

Makes the image occupy the full width of its parent grid item.

**`height: 100%;`**

Makes the image occupy the full height of its parent grid item.

**`object-fit: cover;`**

Fills the available space without stretching or distorting the image.

Some portions may be cropped to ensure the entire grid cell is covered.

**`display: block;`**

Changes the image from its default inline display behaviour to block-level behaviour.

This removes the small baseline gap that can appear underneath inline images.

**`opacity: 0.9;`**

Sets the image opacity to 90%.

This allows the images to blend slightly with the darker background atmosphere.

**`transition: opacity 0.4s ease;`**

Defines how changes to the image opacity should animate.

- `opacity` identifies the property being animated.
- `0.4s` defines the animation duration.
- `ease` defines the transition timing curve.

A transition only becomes visible when the opacity changes. The current stylesheet does not contain a hover rule, so this transition is ready for a future interaction rather than currently producing a hover effect.

**`filter: brightness(0.85) saturate(0.85);`**

Applies two visual filters.

- `brightness(0.85)` reduces image brightness to 85%.
- `saturate(0.85)` reduces colour intensity to 85%.

This creates a slightly darker and less saturated appearance, helping the images blend with the background video.

---

# PART 3: Arranging the Images Using Grid Placement

This section is where the individual images receive their positions and spans.

## 1. The first image

```css
.one {
    order: 1;
    grid-column-start: span 2;
}
```

**`order: 1;`**

Controls the order in which this grid item participates in automatic placement.

Grid items have a default order of `0`.

Items with lower order values are considered before items with higher values.

**`grid-column-start: span 2;`**

Makes this image occupy two columns.

The `span` keyword tells CSS Grid how many tracks the item should cover rather than specifying an exact ending grid line.

## 2. The second and third images

```css
.two {
    order: 2;
}

.three {
    order: 3;
}
```

These rules assign the second and third images their respective ordering values.

They do not specify explicit row or column positions, so CSS Grid's automatic placement algorithm determines where they fit.

## 3. The eighth image

```css
.eight {
    order: -1;
    grid-row-start: 1;
    grid-row-end: 3;
    grid-column-start: 5;
    grid-column-end: 6;
}
```

This is one of the most interesting placements in the project.

**`order: -1;`**

Places this item before the other items in order-modified document order.

**`grid-row-start: 1;`**

Starts the image at the first horizontal grid line.

**`grid-row-end: 3;`**

Ends the image at the third horizontal grid line.

Since the grid has two rows, this makes the image span both rows.

**`grid-column-start: 5;`**

Starts the image at the fifth vertical grid line.

**`grid-column-end: 6;`**

Ends the image at the sixth vertical grid line.

Together, these declarations place the image in the fifth column, spanning the full height of the grid.

## 4. The ninth image

```css
.nine {
    grid-column-start: span 3;
    order: 7;
}
```

**`grid-column-start: span 3;`**

Makes the image occupy three columns.

**`order: 7;`**

Assigns it an order value of seven, placing it later in the automatic placement sequence.

## 5. Additional ordering classes

```css
.seven {
    order: 7;
}

.six {
    order: 6;
}

.five {
    order: 5;
}

.four {
    order: 4;
}
```

These classes assign ordering values to grid items.

The current HTML contains `.seven`, but it does not contain elements with `.six`, `.five` or `.four`.

Therefore, those three rules are currently unused.

The `.seven` and `.nine` elements both have an order value of seven. When order values are equal, their original document order determines their relative order.

### Understanding the Grid placement strategy

The project combines three useful CSS Grid techniques:

1. Automatic placement: Grid positions items when explicit row and column coordinates have not been provided.
2. Spanning: Items can occupy multiple rows or columns.
3. Ordering: The `order` property influences the sequence used by automatic placement.

This combination makes it possible to create an asymmetrical gallery without assigning an exact row and column to every image.

---

# PART 4: What I Learned From This Project

Building this gallery helped me understand how individual CSS properties work together to create a complete layout.

The most important concepts I practised were:

- Creating equal columns and rows using `repeat()` and `1fr`.
- Using `minmax()` to control grid track sizing.
- Using `span` to make grid items occupy multiple columns and rows.
- Using `order` to influence automatic grid placement.
- Using `object-fit: cover` to control image dimensions.
- Using `place-items: center` to centre a layout.
- Using `position: absolute` to layer a background video.
- Using `z-index` to control stacking order.
- Using pseudo-elements to create a dark overlay.
- Using `opacity` and `filter` to adjust image appearance.
- Using viewport units and the `min()` function for responsive sizing.

One particularly useful lesson was understanding that CSS Grid can be used at different levels of a webpage.

In this project, the outer `.page` uses Grid to centre the gallery, while the inner `.container` uses Grid to arrange the images.

This distinction helped me understand Grid as more than a way to create columns and rows. It is also a tool for controlling the overall layout of a webpage.

# Conclusion

This project marks the end of my dedicated CSS Grid practice before moving on to Bootstrap.

My objective was not just to reproduce a visual layout, but to understand the reasoning behind the CSS properties used to build it.

The next step is to explore how Bootstrap provides a structured approach to responsive layouts and reusable interface components.

**Project:** Arcane-Inspired CSS Grid Gallery  
**Technologies:** HTML5 and CSS3  
**Next learning milestone:** Bootstrap
