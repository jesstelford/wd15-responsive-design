# Web Fonts Loading / Performance

The virue of maps, they show what can be done with limimte space, they foresee
that evertyhing can happen therein.

> Many people in the design process simply don't know a lot about performance
> consequences of their design decisions.
- Brad Frost

> There is no difference to a user between a site being down and a site being
> inaccessible due to loading issues. [...]
- ?

## Font formats

WOFF, TTF, EOT, WOFF2, SVG

EOT is only for oldIE (<9)

For just IE9+, you can do:
woff2
woff
otf

## Loading Fonts

Network requests go like:

```
HTML   [--------]
CSS         [--------]
Font 1                [------]
Font 2                [------]
```

Ie; Can't start downloading fonts until after DOM & CSSOM are fully generated.

### Issues

* FOIT (Flash of invisible text): No content visible until font downloads.
* FOUT (Flash of unstyled text): show content in fallback font until font
downloads.

Solution: prioritise content over presentation Display content right away, swap
fonts later:

* First visit show content
* Async load fonts during rendering
* Cache wrb fonts
* Apply web fonts right away (or on later visits to avoid FOUT)
* Apply web fonts only if cached on subsequent visits

### Case study: The Guardian

1. Forked mobile experience.
2. Improved accessibility, etc.
3. Made mobile the tablet experience & monitored how long / hard it took them.
4. Then tablet to desktop, desktop to tv, etc.

* _Priority lists_ for content and styles to define "core":
  * Core content doesn't rely on JavaScript,
  * Only one main feature image considered "core",
  * No ajax support for rating, comments and live scores,
  * "Cutting the mustard" to "buckle" browsres,
  * web fonts aren't loaded by default (to prevent OUT).
* Module loading, 3 types of content:
  1. Core content
    * Essential HTML, CSS, non-JS enhanced experience
  1. Enhancement
    * JS, Geolocation, touch, enhanced CSS, web fonts, etc
  1. Leftover
    * analytics, advertising, third-party content
* Load core content first, then Enhancement on `DOMContentLoaded`, then
  leftovers on `Load`.

Eg: http://speakerdeck.com/andyhume/anatomy-of-a-responsive-page-load

Modular loading:

* Load JS into a browser _async_. While JS is being downloaded, browsre still can
parse the docment and show content.
* HTML/JS (for modern browsers):
  ```
  @if(isModernBrowser) {
    <script src="enhance.js" async defer></script>
  }
  ```

`isModernBrowser()`:

* server-side: UA string detection (DeviceAtlas, WURFL).
* client-side feature detection:
  ```javascript
  if (
    'querySelector' in document
    && 'localStorage' in window
    && 'addEventListener' in window)
  {
    // HTML5 browser
  }
  ```
  or
  ```javascript
  if ('visibilityState' in document) {
    // HTML5 browsre
  }
  ```

Loading web fonts:

if:
* Cut the mustart?
* Support Woff?
* Font cached?
  * Then, you can have the font

Guardian usres need to successfully copmlete ONE HTTP request to read content.
0.798 seconds to load (300ms Round trip time).

http://github.com/guardian/frontend

### Case study: Smashing Magazine

Minor optimization based on a simple principle: optimise content, _defer the
rest_:

* Load critical CSS inline and full CSS on load,
* Avoid _Javascript libraries_ (jQuery -> Javascript)
* Store Web fonts in localStorage + cookies
* Defer advertising, tracking and all non-critical CSS/JS.
  * Did Ad impressions / conversions go down?
    * Yes, when in "leftovers".
    * Yes, but not as much as in "leftovers", *but* _clicks_ increased (because
      they're already engaged with the content)
* Replaced respond.js with IE8 stylesheets (fixed-width)
* Optimize the critical rendering path for content delivery.

See article: Improving smashing magazine's [...]

### Loading critical CSS

Automate it with `criticalcss` / `grunt-criticalcss`

http://github.com/filamentgroup/enhance - "A full-configured `head` setup for
EnahanceJS

http://jalcab.com/localFont or http://jaicab.com/localFont (localhost cache)

or

http://github.com/bramstein/fontfaceobserver (HTTP cache only)

### Pro tips

Keep speed index below 1000.

Make sure first 14kb contains as much CSS / HTML as possible to render the page.
Do this by inlining the first 1200 pixels.

Why 14kb? 1024 bytes per TCP packet. TPC can do 10 packages at a time, so
approximately 14kb.

Use localStorage over http cache for web fonts. Why?:

> Caches dont stay populated for very long. There is a 42% change that any request
will have a cache that is, at most, 47 hours old
- facebook http cache exercise

The way Gmail speeds up their loading:
* Idea: Let browsers download all of the JS right away, but _evaluate it "on
demand"_, i.e. when users need a particular feature.
* Most of the downloaded JS is ommented out, and when needed uncommented and
`eval`-ed
* 200KB of JS went from 2600ms -> 240ms

For social shares & video playing, use a simple image/ button. Then load the JS
once the user actually clicks it.
