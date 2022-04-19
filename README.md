# Frontend Mentor - 3-column preview card component

This is a solution to the [3-column preview card component challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/3column-preview-card-component-pH92eAR2-). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Overview

### The challenge

Build a responsive layout matching the given design.

### Links

- Check out the [solution on Frontend Mentor here](https://www.frontendmentor.io/solutions/responsive-layout-without-media-queries-Hk5KMphV9).
- Check out the [live site here](https://lyons-frontend-mentor.github.io/3-column-preview-card-component/).

### Built with

- HTML
- CSS

## Reflection

For the past week I have been working on [this other, more difficult challenge](https://www.frontendmentor.io/challenges/coffeeroasters-subscription-site-5Fc26HVY6), and at many points in the design I run into the following problem: get a layout with 3 or 4 cards to switch from a column layout (mobile) to a row layout (desktop), with no intermediate layout. This could certainly be accomplished with media queries, but in practice it's difficult to find the correct breakpoint. Instead, I'd like to use a CSS solution which relies on the browser/Flexbox to solve this. 

Thankfully, the excellent book, [Every Layout](https://every-layout.dev/) covers this precise use case, with a layout it calls the "Switcher". The book itself isn't free, and while [the website](https://every-layout.dev/layouts/) has articles on *some* of the layouts for free, you have to get the book to view all of the layouts, including the Switcher. That being said, their Switcher Switcher is based on a [public blog post](https://heydonworks.com/article/the-flexbox-holy-albatross/) from one of the authors, so you can read about everything on the Switcher for free there (I still highly recommend the book, though).

I knew I wanted to use this solution in my solution to the difficult challenge I was working on, but I was having trouble wrapping my head around the Switcher. This is why I chose to work on this simpler challenge, in which the Switcher behavior is precisely the main point of the challenge (at least in my view). At its core (without gutters, differently sized items, etc., the details of which are covered in the aforementioned book and posts), the code for the Switcher is

```
.switcher {
  display: flex;
  flex-wrap: wrap;
}
.switcher > * {
  flex-grow: 1;
  flex-basis: calc((var(--threshold) - 100%) * 999);
}
```

where `--threshold` is a custom property which could be defined elsewhere. 

Essentially, if the width of the `.switcher` element (`100%` from the perspective of its flex children) is greater than `--threshold` width (i.e., if there's enough room for the row layout, whose total width is specified by `--threshold`), then the `flex-basis` value will be a negative value, which is erroneous. CSS will then ignore this line, and the `flex-grow: 1;` will ensure that the flex children take up an equal proportion of the available horizontal space. 

On the other hand, if the width of the `.switcher` element is less than `--threshold` (i.e., there's no room for the row layout), then the `flex-basis` value will be a large positive number, necessitating wrapping. In other words, each flex child will take up its own row (column layout).

All of the  is explained in the book/posts, but it took working through a challenge with the Switcher as the focus for me to really understand it.

### Continued development

Now that I have a better grasp of the Switcher, I feel ready to return to the original challenge I was working on. Moreover, I've seen this pattern several times in Frontend Mentor challenges, so I'm sure it'll help me in future challenges as well.