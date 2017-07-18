#### What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?

- Resetting: Remove all the native styles provided by browsers
- Normalizing: Make the browser styles consistent

#### Describe Floats and how they work.

There are `left`, `right` and `none` for `float`. Each value indicates how an
element should float. When `float` is set, each element will get out of its
normal flow and will be shifted to the specified direction, until it gets its
container or another floated element. Float affects not only  the target element, but also its children.

#### Describe z-index and how stacking context is formed.

The z-index property specifies the stack order of an element, an element with greater stack order is always in front of an element with a lower stack order. Say two DIVs with the same parent, higher z-index will be displayed. It will inherit the z-index property of the parent. Z-index only works on positioned elements (position:absolute, position:relative, or position:fixed). Value can be negative.

#### Describe BFC(Block Formatting Context) and how it works.

BFC is a part of rendering a webpage. It's used to determine from which
positioning and clearing should be done. The context is created by several
ways, but the most famously, by a root element, float, positioned elements.

#### What are the various clearing techniques and which is appropriate for what context?

```css
clear:both;
```

```css
overflow: hidden;
height: auto;
```

#### Explain CSS sprites, and how you would implement them on a page or site.

CSS sprite is combining multiple images into a merged one image and use CSS to
render each of them properly for each element.

It's usually implemented using `background: url(...) x-axis y-axis;`, or
both `background-image` and `background-position`.

#### How do you optimize your webpages for print?

```css
@media print {
  ...
}
```

#### What are some of the "gotchas" for writing efficient CSS?

Usually about CSS selectors.

- Know different browsers have different CSS hacks
- Cater for mobile devices or small screen size
- Good HTML structure and CSS OOP rules with good naming
- Avoid key selectors that match large numbers of elements (tag and universal selectors)
- Prefer class and ID selectors over tag selectors
- Avoid redundant selectors
- Preferably don’t use * (universal selector)
- Use framework (Bootstrap etc.)

#### What are the advantages/disadvantages of using CSS preprocessors?
###### Describe what you like and dislike about the CSS preprocessors you have used.

TO DO.

### How would you implement a web design comp that uses non-standard fonts?

- `@font-face` to write my own `font-family`
- `@import` to import prepared web font(e.g. Google Webfonts)

### Explain how a browser determines what elements match a CSS selector.

Browsers read selectors from right-to-left. First looks for all elements matching the key selector (the right-most). Then checks if it matches or is under the next (left-most) element.

### List as many values for the display property that you can remember.

block, inline, inline-block, none, inherit, table, table-cell, flex

### What's the difference between a relative, fixed, absolute and statically positioned element?

- static: the default one
- relative: relative to its static position
- absolute: you place where you want
- fixed: fixed respect of the viewport of the page. It isuseful when scrolling, for example.

### How is responsive design different from adaptive design?

- Responsive: There is one basic layout, and it changes responsively to
  screen changes
- Adaptive: For each possible screen size, there is a distinct layout.

### Have you ever worked with retina graphics? If so, when and what techniques did you use?

```css
@media (-webkit-min-device-pixel-ratio: 1.25), (min-resolution: 120dpi) {
  ...
}
```
