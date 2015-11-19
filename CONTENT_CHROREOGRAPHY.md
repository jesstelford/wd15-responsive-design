# Content Choreography

## `currentColor` in CSS

Quite well supported. (>= IE9)

Takes the current color from surrounding context and applies it to the element.
No need to use SASS variables, etc.

Allows you to have the border & icon inherit the colour of the text on a button
(for example).

## Long words

```css
overflow-wrap: break-word
word-wrap: break-word
```

## Nested links

Normally a browser will think you've given it broken html, so will split the
link.

But if you wrap the nested link in an `<object>` tag, the browser will:

* Ignore it like it exists outside the DOM
* Will create separate links as you expect

Eg;

```html
<a href="">Blah foo <object><a href="">Inner link</a></object></a>
```

## Flexbox

Supports >= IE11 (partial IE9) (But can support floats, etc, as fallback)

http://jordanm.co.uk/lab/contentchoreography/

Flexbox tries to solve 2 things:

* Source order
* Intermixing content

### Source Order

In a "linearized" layout, content blocks are displayed in the source order by
default.

But not with flexbox!

```css
#main { display: flex }

#main > nav { flex: 1 }
#main > aside { flex: 1 }
#main > article { flex: 2 }

@media screen and (max-width: 20em) {
  #main > article { order: 0 }
  #main > aside { order: 1 }
  #main > nav { order: 2 }
}
```

```
 -----------------------------
|         <header>            |
 -----------------------------
| <nav> | <article> | <aside> |
 -----------------------------
|         <footer>            |
 -----------------------------
```

`order` gives the order of display

`flex` is a way to split up as "shares" (so in the above example, there are a
total of 4 "shares" [1 + 1 + 2], so the total space is split into that many
equal spaces, then assigns them to those spaces)

Note: Child items do not inherit `display: flex` from their parent.

---

Flexbox foundation

* Directional (main / cross axis) (main defaults to x, cross defaults to y)
* Wrapping defined with `flex-wrap`
  * Controls whetever flex items can take up multiple rows
* Sizing defined with `flex` shortcut
  * shortcut for `[flex-grow] [flex-shrink] [flex-basis]`
  * `flex-grow`: how much flex item will grow relative to other items if extra
    space is available (proportion of extra space that it gets). Ie; if it is
    set to `5`, and others to `1`, will be allocated _extra space_ 5 times
    faster than others.
  * `flex-shrink`: Reverse of `flex-grow`.
  * `flex-basis`: the initial starting size before free space is distributed (any
    standard width/height value, including `auto`). Kind of like `min-width`.
* Alignment defined across main / cross axis

Goal: Can avoid media queries with flexbox.

Make sure you use `box-sizing: border-box` so you don't get weird sizing issues
with padding and border etc.

Now: `margin-top: auto` works with flexbox when you have extra space.

When in doubt: Add more `display: flex`!

Flexbox overwrites everything except absolute positioning.

When using flexbox, be sure to provide an undo for any margins required when
floating, etc.

Use `@supports` CSS property to check if flexbox is supported (aka "CSS Feature
quieries"). No IE support. (So, can still use modernizr)

For the ultimate fallback (eg: email): "CSS Stacking with display:table" - iandevlin.com

### Example

http://codepen.io/anon/pen/JoBKgK
