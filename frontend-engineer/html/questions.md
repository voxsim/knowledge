## What are data- attributes good for?
Just to store additional informations.

## Consider HTML5 as an open web platform. What are the building blocks of HTML5?
This question is a bit confusing, as when you say building blocks, my head goes to block elements. The HTML5 specific ones are:
- `<article>`
- `<aside>`
- `<audio>`
- `<canvas>`
- `<figcaption>`
- `<figure>`
- `<footer>`
- `<header>`
- `<hgroup>`
- `<output>`
- `<section>`
- `<video>`
The numerous APIs and the more semantic tags, could also be said to be the building blocks.

## Describe the difference between a cookie, sessionStorage and localStorage.
Cookie:
- Max size of 4093 bytes
- Can set expiration date
- Sent on every request

sessionStorage:
- Max size of 2.5MBs+ depending on browser
- Stored in browser and not sent with every request
- If you close a tab using sessionStorage, open a new tab, or exit the browser -> you'll lose that specific sessionStorage data.

localStorage:
- Max size of 2.5MBs+ depending on browser
- Stored in browser and not sent with every request
- Will persist if browser/tabs are closed.

## Describe the difference between <script>, <script async> and <script defer>
- A regular <script> tag will block rendering of the page, and the page will not continue to load until the script finishes.
- <script async> will run the script asynchronously, meaning that it will not block rendering, but will run as soon as the script is available. This is usually intended for CDN files, or other such files, which do not change the page structure.
- <script defer> will defer the script to run after the page is done parsing and before an onload event.

## Why is it generally a good idea to position CSS <link> between <head></head> and JS <script> just before </body>? Do you know any exceptions?

You usually put the <link> tags in between the <head> to prevent Flash of Unstyled Content which gives the user something to look at while the rest of the page is being parsed.

Since Javascript blocks rendering by default, and the DOM and CSSOM construction can be also be delayed, it is usually best to keep scripts at the bottom of the page.

Exceptions are if you grab the scripts asynchronously, or at least defer them to the end of the page.

## What is progressive rendering?
With HTML progressive rendering is chunking the HTML into separate bits and loading each block as it's finished. Usually, the backend code loads the HTML at once, but if you flush after finishing one part of the structure, it can be rendered immediately to the page.

This can be done asynchronously with different components being loaded as they finish. There's new features which can be used with Web Components making it more standard. Another interesting article on this is from eBay with Async Fragments.

## Semantic Elements
A semantic element clearly describes its meaning to both the browser and the developer.
- Examples of non-semantic elements: `<div>` and `<span>` - Tells nothing about its content.
- Examples of semantic elements: `<form>`, `<table>`, and `<article>` - Clearly defines its content.

HTML5 offers new semantic elements to define different parts of a web page:  
- `<article>`
- `<aside>`
- `<details>`
- `<figcaption>`
- `<figure>`
- `<footer>`
- `<header>`
- `<main>`
- `<mark>`
- `<nav>`
- `<section>`
- `<summary>`
- `<time>`

## What's the difference between HTML and XHTML?

HTML:
- Start tags are not required for every element.
- End tags are not required for every element.
- Only void elements such as br, img, and link may be “self-closed” with />.
- Tags and attributes are case-insensitive.
- Attributes do not need to be quoted.
- Some attributes may be empty (such as checked and disabled).
- Special characters, or entities, do not have to be escaped.
- The document must include an HTML5 DOCTYPE

XHTML:
- All elements must have a start tag.
- Non-void elements with a start tag must have an end tag (p and li, for example).
- Any element may be “self-closed” using />.
- Tags and attributes are case sensitive, typically lowercase.
- Attribute values must be enclosed in quotes.
- Empty attributes are forbidden (checked must instead be checked="checked" or checked="true").
- Special characters must be escaped using character entities.
