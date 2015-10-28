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

http://bradfrost.com/blog/post/atomic-web-design/

Atoms, Molecules, Organisms, Templates, Pages

We think about the page at the very end of the process. _Not_ at the start.

Thinking about the page first? It's a trap! You end up designing pages in
different views (phone, tablet, desktop, TV, etc). Takes way too much time.

But, if you think about pages last, the organisms are easier to change early on.

> Organise your UI libraries in _small elements_, then work your way out toward
> larget copmonents, and _then_ layouts. While doing that, always be explicit
> about all objects' associated types, variants and states.
- Jina Bolton

UI Stack has layers, each is a state:
* Blank
* Lodaing
* Partial
* Error
* Ideal

Difficult to do with photoshop / fireworks mockups, etc. But easier in HTML, so
when do you move to HTML mockups?

Pattern libraries (eg; a listapart / bootstrap) feel nice.
But it doesn't give the "bigger picture".

So, how do we do it?

> 1. *Designing in text editor first* forces you to full understand and
> formulate goals, _objectives_ and the _language_ of a project.

Eg: A `.md` doc.

Really forces you to think about the core content.
Also exactly what you want to acheive with the page.

Then easy to move into a UX sketch.

> 2. *Visual invetory* helps to _decide on visual direction_ without spending
> too much time on "deadlift" mock-ups.

Library of a bunch of website screenshots, etc.
Wen taling to client, can pick a few different screenshots from library, write
some notes, then share with client to help determine visual direction.

_A little trick_: If you want to spark a discussion with a client. Just put the
client's logo in the top-left: They'll immediately associate with the design /
brand, greatly speeding up the decision time.

Start with the core part first. Eg; donation form on a charity website. Think
about the atoms / molecules.

> 3. *Project hub* is one central place where the most important things go

http://superfriend.ly

The client can go there check the status, etc. Sorted Chronologically

* Performance
* User interviews
* mockups.

Don't show the client a page mock-up. Show them an export of all the salient
components dumped onto one page. This shows visual direction & ideas.

This is just the visual step.


> 4. *Pattern Libraries* establish a _shared design vocabulary_; it enhances
> consistency and maintainability of a project.

Hard to make sure it stays up to date (maybe a 6 month lifespan)

The guides, notes, pixel counts, etc, the designers hand-off are only for the
absolute perfect case. There's no trust in the developer. "I'm going to make
everything so pixel perfect that you can't mess it up".

But it takes so much time!

What's the alternative?

We have some beautiful design made by the designer.
But, as a developer, here's what you're going to get:

*Vocabulary*

* Discover and define a shared vocab for modules
  * Can be from Design or Frontend perspective, both are valid
* Make the vocab part of everyday culture

Eg; Intros & Outros vs Header / Footer. Or Heros, Bridges (connect other
components; pagination). Or Helpers (next to components, but not connected like
a bridge)

*Grammar*

* Identify simple rules on how parts fit gotegher
* The language is refined during prototyping

Eg: a rule is: "Horizontal spacing between modules is always two columns
(+gutter) within the responsive grid"

Removes the need to annotate a photoshop mockup.

The photoshop mockup becomes mostly just for designers, but not to be sent to
devs.

Responsive Layout Behaviour diagram: Pick a page (eg; a product details page).
Start thinking about the grid, layout, everything that has to go on the page.
Create a diagram with breakpoints on horizontal axis, components on vert axis:

```
       |  xs   | small | medium | large | x-large | xx-large |
intro  | <- stacked -> | <--- two-column -------> | <------> |
```

States, usage notes, hints, added to the code. Then can feed that into the
living style-guide which is extracted by running phantomjs over your code. Eg:
Pattern Lab, KSS, etc.

Good to add performance indicators, interactions, etc.

"Styleguide & Boilerplate Patterns Spreadsheet" - great for finding a framework
that has a particular component which you can slap togeter into a HTML mock-up.

http://styleguides.io

*Language*

* Design assemby of flexible, distinct

*Gotchyas*

_Single maintainer_

When there's just 1 person maintaining a pattern library - they will eventually
not be able to maintain it anymore, and will become the bottleneck. Eventually
the maintenance will stop all together.
So, you need every developer to be responsible.

_Remote teams_

Have to keep the code constantly up to date.

"A Maintainable Style Guide" - Iean Feather

REST API calls:

```
ui_component("forms/search", {label: "Search"})
// output:
<form> ... </form>
```

Even if the styleguide changes, the library is automatically updated behind the
REST API, so you never fall behind.

Eg; "rizzo" by lonelyplanet: http://github.com/lonelyplanet/rizzo

_Automate core / settings_

Or, taking it even further:

http://github.com/salesforce-uix/theo

Single source of truth where yo uwrite a config file that defines rules.

Any changes in this config will filter all the changes down through all the code
(css, ios, android), etc.

_Trying text changes_

Add `contenteditable=true` to the `<html>` element so client, marketing, etc can
edit whatever they want on the page.

_Disconnect between design & implementation_

Translating CSS changes back into photoshop design.

Use a tool called "Pagelayers" - you don't have to maintain a photoshop file
anymore. ("Paparatizi" for Sketch)

Open any page, exports every div into photoshop layers. Make some changes, show
the dev the changes, then throw the photoshop file away. (Need more changes?
Just re-export).

_(no #5?)_

> 6. *Redesigns* usually follow exactly the same process, but usually an
> _interfacte inventory_ is made from existing page.

