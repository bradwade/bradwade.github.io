---
layout: article
title: Maintain Aspect Ratio of Background Image
categories: front-end
comments: true
share: true
image:
  teaser: lock-400-250.jpg
  feature: lock-1140-285.jpg
  credit: Joshua Brandenburg
  creditlink: http://www.drinkandsmile.com/
excerpt: A look at a couple of methods for a div to maintain the aspect ratio of a background image. Also a sass mixin for my preferred approach. 

---

At times we want to have the div of a background image maintain the same aspect ratio as the image in the background. The most common use case for this I have encountered is when creating a full-width hero/masthead with a background image and text overlayed on top. 

Here are a couple of ways to approach this.

## vw method

If the width of the box is 100% of the viewport, you can use a height with a vw value. (1vw is 1/100th of the width of the viewport.)
  
Advantages:

- No extra wrappers necessary. 
- Less scss.

Disadvantages:
  
- less browser compatible (no IE8 and below) 
- (In Chrome at least) vw includes the scrollbar in the calculation, so the ratio is not perfect when scrollbars are present.

## padding/absolute method

Using an extra wrapper, padding on a before pseudo class and absolutely positioning the inner div method.
    
This works because a padding percentage (even for top or bottom padding) is calculated based on the WIDTH of the element.

Advantages:

- Greater browser compatibility.
- Not limited to full viewport width. (Can be used at any width.)

Disadvantage: 

- Extra inner wrapper required.

## Mixin

Here is the mixin I wound up using for the padding/absolute method. Watch out for the assumed inner div that is absolutely positioned. You may want to use a specific class name there such as `.inner-wrapper` instead of just `> div`.

{%highlight scss %}
@mixin aspect-ratio($width, $height) {
  position: relative;
  &:before {
    display: block;
    content: "";
    width: 100%;
    padding-top: ($height / $width) * 100%;
  }
  > div {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
}
{% endhighlight %}

Then simply call the mixin when needed...

{%highlight scss %}
.my-masthead-div-with-background-image {
  @include aspect-ratio(8,1);
}
{% endhighlight %}

## Experiment around with the techniques...

Edit this CodePen and change the scss values to see it in action.

<p data-height="268" data-theme-id="0" data-slug-hash="NGXVpg" data-default-tab="result" data-user="bradwade" class='codepen'>See the Pen <a href='http://codepen.io/bradwade/pen/NGXVpg/'>Maintaining Aspect Ratio</a> by Brad Wade (<a href='http://codepen.io/bradwade'>@bradwade</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>
