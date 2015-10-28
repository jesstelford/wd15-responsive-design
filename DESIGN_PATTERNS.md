# Responsive Design Patterns

## Responsive Icons

Important for logos to send different assets to different screen sizes.

Strategies:
* Some complex logos might need modification / simplification for smaller sizes.
* Shift the position of the logo
  * Eg; from above text, to the side of text

Don't forget to target height for mobile (eg; landscape mobile vs portrait table
is very different)

## Responsive Tables

Allow user to select which columns to see.

Provide "focus" mode where you can highlight a row when tapped. Eg;
http://gergeo.se/RWD-Table-Patterns

Try re-think the display of the table data. Maybe allow user to switch to
pie-chart on mobile?

Another option: Tilting headers by 45degrees when screen a lot thinner (eg; for
flight booking websites, etc)

http://Swiss.com air inverts the table, and accordians the data on mobile.

### Calendars

Harder, more specific use case.

* Move from month > week > day as screen gets smaller
* Shrink calendar to be just icons on each day, sitting on top of an agenda
  list.

http://bigfootjs.com

## Responsive pdf

Generate low res jpegs of each page for thumbnails, then higher res ones when
the user zooms.

## Responsive maps

* Small vs vs large view option.
* Group options, then provide pop-up list to select which they wanted to click.

But what about when the user scrolls over a map, which captures input?

* Invisible div which goes away when clicked
* Small image thumbnail which triggers load of map

When you have lots and lots and lots of elements. Canvas + tiles works really
really well. Only re-render the area the user is interacting with.

Eg; http://seatgeek.com
"High Performance Map Interactions Using HTML5 Canvas" - "ChairNerd" Aug 18th,
2014.

## Responsive lightboxes

Clicking an image to see it bigger should NOT make it smaller (because: lightbox
borders).

If you don't have space to show lightbox, take user to a new page. If you do,
show it.

## Typography

"On the typography of flight-deck documentation" - NASA, 1992

Viewing distance is an important factor.

Netflix: Relationship between height of movie cover and viewing distance. Using
CSS inches measurements: 0.5" of height per foot of viewing distance

"maratz" realtime typography zooming example.
