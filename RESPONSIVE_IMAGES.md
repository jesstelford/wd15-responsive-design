# Responsive Images

## Non-responsive images

Aftonbladet's Images Strategy:

* Double image size, then really compress Jpeg image (eg; 30%), but display at
  1/2 the size on screen - user can't tell the difference
* "large" screen has 650KB worth of images
* Some parts of image don't compress very well, but it's a tradeoff
* Blurring some background details can compress better still

## Responsive Images

Different images to different screens.

What about 4k screens?
* iOS has a 3 megapixel resource limit

*Tim Kadlec "Media Query Asset Downloading" article*

`display: none` on images with media queries will cause ALL browsers to request
ALL versions of the files. Same for background image.

_BUT_ Creating an empty div inside, but then wrap in a div which has `display:
none` and a background-image.

Whoa, this is getting too hacky :(

### Good News

Original `srcset` proposal didn't make it (too complex) (see
http://xanthir.com/b45u0 )

### Bad News

The main issue with responsive images is the variaty of use-cases we ave to
cater to:

* Render crisply on all pixel densities
* Adjust fludly to layout
* Adapt images beyond scaling (eg; crop particular section of picture, etc)
* Deliver different image formats to different browsers

Problem: How do we manage all 4 at one time?

Browsers know:
* Viewport size
* Screen density

Designers know:
* Rendered size
* image size

How it works:

* Render crisply on all pixel densities
  * `srcset` is a hint to the browser about which image to get (meta info)
    * `<img srcset="small.jpg 1x, large.jpg 2x" src="small.jpg" />`
  * Always falls back to `src=""` in `<img>` tag.
  * Up to the browser to select which image based on things like connection
    speed, retina screen, etc
* Adjust fludly to layout
  * `sizes` Can take media-querly like things to specify how to show it:
    * `sizes="(min-width: 36em) 33.3vw, (min-width: 55em) 50vw, calc(100vw - 2.5em)"`
* Adapt images beyond scaling (eg; crop particular section of picture, etc)
  * `<picture>` element gives you more control than `srcset` on `<img>`
    * Also has a `media="(min-width: 36em)"` attribute on the `<source>`
* Deliver different image formats to different browsers
  * Using `<picture>` again, you can specify `<source type="image/webp" ...>`

*NOTE*: Can't style a `<picture>` directly. Have to target the `<img>` inside
it.

Article: "Responsive Images in practice" - A List Apart

Polyfill: http://scottjehl.github.io/picturefill
(But not really necessary as you can just fallback to a `<img>` tag)

Grunt plugin: http://github.com/miller/grunt-responsive-images-converter

### Alternatives

#### Clown Car Technique (with SVG)

http://github.com/estelle/clowncar

Have to use `<object>` instead of `<img>`.

Good things:

* Media queries are based on the parent container rather than the window /
  viewport
* Everything is contained in Clown Car
