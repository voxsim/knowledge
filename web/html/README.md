HyperText Markup Language, commonly referred to as HTML, is the standard markup language used to create web pages. Web browsers can read HTML files and render them into visible or audible web pages. HTML describes the structure of a website semantically along with cues for presentation, making it a markup language, rather than a programming language.

A basic HTML document looks like this:

```html
<!DOCTYPE html>
<html lang="en">
 <head>
  <title>Sample page</title>
 </head>
 <body>
  <h1>Sample page</h1>
  <p>This is a <a href="demo.html">simple</a> sample.</p>
  <!-- this is a comment -->
 </body>
</html>
```

HTML documents consist of a tree of elements and text. Each element is denoted in the source by a start tag, such as "<body>", and an end tag, such as "</body>". (Certain start tags and end tags can in certain cases be omitted and are implied by other tags.)

Tags have to be nested such that elements are all completely within each other, without overlapping:
```html
<p>This is <em>very <strong>wrong</em>!</strong></p>
<p>This <em>is <strong>correct</strong>.</em></p>
```

This specification defines a set of elements that can be used in HTML, along with rules about the ways in which the elements can be nested.

Elements can have attributes, which control how the elements work. In the example below, there is a hyperlink, formed using the a element and its href attribute:
```html
<a href="demo.html">simple</a>
```

Attributes are placed inside the start tag, and consist of a name and a value, separated by an "=" character. The attribute value can remain unquoted if it doesn't contain ASCII whitespace or any of " ' ` = < or >. Otherwise, it has to be quoted using either single or double quotes. The value, along with the "=" character, can be omitted altogether if the value is the empty string.

```html
<!-- empty attributes -->
<input name=address disabled>
<input name=address disabled="">

<!-- attributes with a value -->
<input name=address maxlength=200>
<input name=address maxlength='200'>
<input name=address maxlength="200">
```

HTML user agents (e.g. Web browsers) then parse this markup, turning it into a DOM (Document Object Model) tree. A DOM tree is an in-memory representation of a document.

DOM trees contain several kinds of nodes, in particular a DocumentType node, Element nodes, Text nodes, Comment nodes, and in some cases ProcessingInstruction nodes.

The document element of this tree is the html element, which is the element always found in that position in HTML documents. It contains two elements, head and body, as well as a Text node between them.

There are many more Text nodes in the DOM tree than one would initially expect, because the source contains a number of spaces and line breaks that all end up as Text nodes in the DOM. However, for historical reasons not all of the spaces and line breaks in the original markup appear in the DOM. In particular, all the whitespace before head start tag ends up being dropped silently, and all the whitespace after the body end tag ends up placed at the end of the body.

The head element contains a title element, which itself contains a Text node with the text "Sample page". Similarly, the body element contains an h1 element, a p element, and a comment.

This DOM tree can be manipulated from scripts in the page. Scripts (typically in JavaScript) are small programs that can be embedded using the script element or using event handler content attributes.

HTML documents represent a media-independent description of interactive content. HTML documents might be rendered to a screen, or through a speech synthesizer, or on a braille display. To influence exactly how such rendering takes place, authors can use a styling language such as CSS.

## Block Elements (also called “flow content”)
Block-level elements are always drawn on a new line after them.

### Paragraphs
The `<p>` element marks all the text inside it as a distinct paragraph.

### Headings
Headings are like titles, but they're actually displayed on the page. HTML provides six levels of headings, and the corresponding elements are: `<h1>`, `<h2>`, `<h3>`, … , `<h6>`. The higher the number, the less prominent the heading.

### unordered lists
Whenever you surround a piece of text with HTML tags, you’re adding new meaning to that text. Wrapping content in `<ul>` tags tells a browser that whatever is inside should be rendered as an “unordered list”. To denote individual items in that list, you wrap them in `<li>` tags

### ordered lists
With an unordered list, rearranging the `<li>` elements shouldn’t change the meaning of the list. If the sequence of list items does matter, you should use an “ordered list” instead. To create an ordered list, simply change the parent `<ul>` element to `<ol>`.

## Inline Elements
Inline elements can affect sections of text anywhere within a line.

### emphasis (italic) elements
For instance, `<p>` is a block-level element, while `<em>` is an inline element that affects a span of text inside of a paragraph. It stands for “emphasis”, and it’s typically displayed as italicized text.

### strong (bold) elements
If you want to be more emphatic than an `<em>` tag, you can use `<strong>`. 

## Empty html elements
The HTML tags we’ve encountered so far either wrap text content (e.g., `<p>`) or other HTML elements (e.g., `<ol>`). That’s not the case for all HTML elements. Some of them can be “empty“ or “self-closing”. Line breaks and horizontal rules are the most common empty elements you’ll find. The trailing slash (/) in all empty HTML elements is entirely optional.

### Line breaks
To tell the browser that we want a hard line break, we need to use an explicit `<br/>` element.

### Horizontal rules
The `<hr/>` element is a “horizontal rule”, which represents a thematic break. The transition from one scene of a story into the next or between the end of a letter and a postscript are good examples of when a horizontal rule may be appropriate.

## Links/Anchors
Links are created with the `<a>` element, which stands for “anchor”.

There are three types of links:
- Absolute links: they are the most detailed way you can refer to a web resource. They start with the “scheme” (typically http:// or https://), followed by the domain name of the website, then the path of the target web page.
- Relative links: they point to another file in your website from the vantage point of the file you’re editing.
- Root-relative links:  They are similar to the relative links, but instead of being relative to the current page, they’re relative to the “root” of the entire website. They begin with slash ('/').

Attributes alter the meaning of HTML elements, and sometimes you need to modify more than one aspect of an element. For example, <a> elements also accept a target attribute that defines where to display the page when the user clicks the link. By default, most browsers replace the current page with the new one. We can use the target attribute to ask the browser to open a link in a new window/tab.

## Images
Unlike all the HTML elements we’ve encountered so far, image content is defined outside of the web page that renders it. Fortunately for us, we already have a way to refer to external resources from within an HTML document: absolute, relative, and root-relative URLs.

Images are included in web pages with the `<img/>` tag and its `src` attribute, which points to the image file you want to display.

### Image formats
There’s four main image formats in use on the web, and they were all designed to do different things. Understanding their intended purpose goes a long way towards improving the quality of your web pages.

#### JPG images
JPG images are designed for handling large color palettes without exorbitantly increasing file size. This makes them great for photos and images with lots of gradients in them. On the other hand, JPGs don’t allow for transparent pixels.

#### GIT images
GIFs are the go-to option for simple animations, but the trade off is that they’re somewhat limited in terms of color palette—never use them for photos. Transparent pixels are a binary option for GIFs, meaning you can’t have semi-opaque pixels. This can make it difficult to get high levels of detail on a transparent background. For this reason, it’s usually better to use PNG images if you don’t need animation.

#### PNG images
PNGs are great for anything that’s not a photo or animated. For photos, a PNG file of the same quality (as perceived the human eye) would generally be bigger than an equivalent JPG file. However, they do deal with opacity just fine, and they don’t have color palette limitations. This makes them an excellent fit for icons, technical diagrams, logos, etc.

#### SVG images
Unlike the pixel-based image formats above, SVG is a vector-based graphics format, meaning it can scale up or down to any dimension without loss of quality. This property makes SVG images a wonderful tool for responsive design. They’re good for pretty much all the same use cases as PNGs, and you should use them whenever you can.

There is one potential issue with SVGs: for them to display consistently across browsers, you need to convert any text fields to outlines using your image editor. If your images contain a lot of text, this can have a big impact on file size.

### Define dimensions
By default, the `<img/>` element uses the inherit dimensions of its image file. To get our pixel-based images down to the intended size (75×75), we can use the `<img/>` element’s width attribute. The width attribute sets an explicit dimension for the image. There’s a corresponding height attribute, as well. Setting only one of them will cause the image to scale proportionally, while defining both will stretch the image. 

### Text alternatives
Adding alt attributes to your <img/> elements is a best practice. It defines a “text alternative” to the image being displayed. This has an impact on both search engines and users with text-only browsers (e.g., people that use text-to-speech software due to a vision impairment).

## Document language
A web page’s default language is defined by the lang attribute on the top-level <html> element. Our document is in English, so we’ll use the en country code as the attribute value (do this for all of the pages we created):

```html
<html lang='en'>
```

If you’re not sure what the country code for your language is, you can look it up [here](http://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) under the Subtag field.

### How do you serve a page with content in multiple languages?
By changing the lang attribute on the html element.

```html
<!-- HTML -->
<html lang="en">

<!-- XHTML -->  
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">  
```

Elements can also be wrapped in a lang tag if you have more than one language on the same page.

```html
<div lang="es">Yo no hablo español</div>  
<div lang="fr">Je ne parle pas français</div> 
```

## Character sets
A “character set” is kind of like a digital alphabet for your browser. It’s different from the language of your document in that it only affects how the letters themselves are rendered, not the language of the content.
When you use special characters you will see weird stuff because the default character set for most browsers doesn’t accommodate these one. To fix this, specify a UTF-8 character encoding by adding a <meta> element with a charset attribute to the <head> of our misc/extras.html file:

```html
<meta charset='UTF-8'/>
```

The special characters should now render correctly. These days, UTF-8 is sort of like a universal alphabet for the Internet. Every web page you create should have this line in its <head>.

## Reserved characters
The <, >, and & characters are called “reserved characters” because they aren’t allowed to be inserted into an HTML document without being encoded. This is because they mean something in the HTML syntax: < begins a new tag, > ends a tag, and, as we’re about to learn, & sets off an HTML entity.
Entities always begin with an ampersand (&) and end with a semicolon (;). In between, you put a special code that your browser will interpret as a symbol. In this case, it interprets lt, gt, and amp as less-than, greater-than, and ampersand symbols, respectively. There’s a lot of HTML entities, see https://dev.w3.org/html5/html-author/charref.

## DocType

A DOCTYPE is a required preamble.

DOCTYPEs are required for legacy reasons. When omitted, browsers tend to use a different rendering mode that is incompatible with some specifications. Including the DOCTYPE in a document ensures that the browser makes a best-effort attempt at following the relevant specifications.

In HTML5, the only purpose of the DOCTYPE is to activate full standards mode. Older versions of the HTML standard gave additional meaning to the DOCTYPE, but no browser has ever used the DOCTYPE for anything other than switching between quirks mode and standards mode.

## Quirks Mode and Standards Mode

In the old days of the web, pages were typically written in two versions: One for Netscape Navigator, and one for Microsoft Internet Explorer. When the web standards were made at W3C, browsers could not just start using them, as doing so would break most existing sites on the web. Browsers therefore introduced two modes to treat new standards compliant sites differently from old legacy sites.

There are now three modes used by the layout engines in web browsers: quirks mode, almost standards mode, and full standards mode. In quirks mode, layout emulates nonstandard behavior in Navigator 4 and Internet Explorer 5. This is essential in order to support websites that were built before the widespread adoption of web standards. In full standards mode, the behavior is (hopefully) the behavior described by the HTML and CSS specifications. In almost standards mode, there are only a very small number of quirks implemented.

## XHTML

If you serve your page as XHTML using the application/xhtml+xml MIME type in the Content-Type HTTP header, you do not need a DOCTYPE to enable standards mode, as such documents always use full standards mode. Note however that serving your pages as application/xhtml+xml will cause Internet Explorer 8 to show a download dialog box for an unknown format instead of displaying your page, as the first version of Internet Explorer with support for XHTML is Internet Explorer 9.

If you serve XHTML-like content using the text/html MIME type, browsers will read it as HTML, and you will need the DOCTYPE to use standards mode.
