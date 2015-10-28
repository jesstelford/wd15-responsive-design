# Resolution Independence

Future proof for resolutions.

svg & icon fonts are both valid.

# svg

svg is very similar to html (doctype, `<g>` == `<div>`, etc, xml syntax)

Conversion from font icon: grumpicon (also generates a fallback?)

Skype has a new smiley `(sarcastic)` (it's a slow cap)

## Embedding

* `<img src="image.svg" />` or `background: url(image.svg);`
  * Can't style the svg because the page doesn't have access to it (think of it
    as an iframe)
* Use inline SVG tag, or base64 encode in css
  * Ugh; no caching
* Use `<object type="image/svg+xml" data="image.svg" class="logo"><!-- fallback image in css --></object>`

## vs icon fonts

You can get the same "sprite" system with svg as with icon fonts.

Create a series of individual svg files, bundle them into one svg file by
wrapping each elmement into a `<g id='icon-calendar'>...</g>` and outputting a
single svg, then use it like:

```html
<svg viewbox="0 0 100 140"><use xlang:href="#icon-calendar"></svg>
```

(or alternatively, have sketch output the viewbox for you)

Tool: `grunt-svgstore`

### Downsides of icon font

Uses unicode code pont, so you could end up colliding with an emoji, or symbol.
Screen readers would also read out the unicode's description.

But, it _is_ possible: 
* "Bulletproof accessible icon fonts" - Filament group
* http://github.com/filamentgroup/a-font-garde

## Pro Tips

JPG image + PNG mask in svg for alpha to greatly reduce the filesize over just a
semi-transparent PNG on its own.

Use `svgo` to optimize your svg files.

```css
img {
  object-fit: cover;
}
```

Will zoom just enough to have the image centered and fitting container

http://github.com/anselmh/object-fit polyfill
