# Vitaly Freedman

## Responsive Design

Collaborative Note Taking: http://www.smashed.by/sydney

2 main problems in Responsive Design:

* Workflow / Teamwork
* Performance

This workshop is about techniques.
And about clever design patterns.
And what works in real-life projects.

### Workflow

Designing Systems, not just pages.

Eg; Style Guides.

Why do a Homer Simpson in CSS? Because it pushes the boundaries.

Think about the old Teletype systems:
* It's a box with content
* Logo
* Navigation (via typing in numbers)
* The original pixel pushers (1 by 1 pixel art)
* Then: Colour. All the extra combinations.
* Resulted in complex artworks, experimentaiton, etc
* Resulted in the "teletext" tool
  * Essentially the original style guide
  * Typography, colours, logos, layouts, etc

But the web...
* It's like box inception - boxes everywhere! Not just the screen-as-a-box.
* Screenshots on devices don't show us anything about experience, etc.
* This is just designing pages, not systems.

> Designing for the Web is like visualizing a _tesseract_. We build experiences by
manipulating their shadows
- Tim Brown

"Making it responsive" is the big unknown in most projects - how long will it take?

#### Responsive Condsiderations

* Components
  * Grid
  * Navigation
  * Form Controls
  * Etc
* Strategy
  * Responsive images (working with legacy CMS, etc)
  * Responsive Typography
  * Interaction/animation
  * Responsive ads
* Layouts
  * Homepage, FAQ, Subpages, etc

Proxy Browsers (eg; Opera Mini)
  * Converts a page into an image with some clickable areas etc
  * JS support is non-existant
  * UC Browser
    * feature testing. Everything is "supported" but in reality it's got no
      support at all

Remembering all of this is super hard. Infact, you're a super-man/woman if you
can!

#### Atomic Design

Atoms, Molecules, Organisms, Templates, Pages

We think about the page at the very end of the process. _Not_ at the start.

Thinking about the page first? It's a trap! You end up designing pages in
different views (phone, tablet, desktop, TV, etc). Takes way too much time.

But, if you think about pages last, the organisms are easier to change early on.

> Organise your UI libraries in _small elements_, then work your way out toward
> larget copmonents, and _then_ layouts. While doing that, always be explicit
> about all objects' associated types, variants and states.
- Jina Bolton
