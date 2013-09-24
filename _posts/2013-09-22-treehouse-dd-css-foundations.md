---
layout: post
title: Treehouse DD CSS Foundations
tagline: Getting up to speed with CSS3
---
{% include JB/setup %}

Mozilla CSS reference: <https://developer.mozilla.org/en-US/docs/Web/CSS/Reference>

## Stylesheet types

* user-agent stylesheets (built into the browser)
* user stylesheets
* author stylesheets

## Selectors
### Universal selector
The universal selector `*` is very powerful and can be used to select **all** elements. Useful for removing all margins and paddings from user-agent stylesheets.

### Type selectors
e.g. body, h1, table

### Descendant selectors
Only select elements which are decendants of other elements.

{% highlight css %}
h1 span { color: blue;}  
.base p { padding: 5px;}
{% endhighlight %}

### Class and ID selectors

Both a class and an ID can be applied to an element. IDs carry more specificity than classes, so styles defined in IDs will carry more weight than styles defined in classes.

### Combinators

Selectors can be combined using a combinator.

#### Direct child

`>` selects elements which are only direct children of the element on the left

{% highlight css %}
h1 > a { color: blue;}  
{% endhighlight %}

#### Adjacent sibling

`+` selects elements which are immediately adjacent to the element on the left

{% highlight css %}
h2 + p { font-size: 1.2em; } 
{% endhighlight %}

#### General sibling

`~` selects all sibling elements, not only those immediately adjacent, to the element on the left. **Note** it will select all elements which follow as long as they are siblings (i.e. on the same level) even if they are separated by other elements, but no elements which are before.

{% highlight css %}
h2 ~ p { font-size: 1.2em; } 
{% endhighlight %}

### Attribute selectors

Select all elements which have a certain attribute.

* `[class]` will select all elements with a `class` attribute (regardless of value)
* `a[class]` will select all `a` elements with a `class` attribute
* `a[class="foo"]` will select all `a` elements with a `class` attribute which has a value of `foo`. **Note** in this example this is much more work for the browser than simply using the `.foo` selector. A better example would be selecting all `input` values of type text, or all anchor tags which open in a new window.

Attribute selectors have the same specificity as classes and pseudo classes.

### Pseudo classes

* `a:link` selects anchor elements which have yet to be clicked on. It can only be used to target anchor elements with the href attribute.
* `a:visited` selects anchor elements which have already been visited.
* `a:hover` select anchor elements which are currently being hovered over. The `:hover` pseudo class can be applied to any element, not just anchors.
* `:active` pseudo class selects elements when they are "active", and can also be applied to any element, commonly applied to anchors.
* `:focus` only applies to interactive elements e.g. links and form elements and can be applied when this element has the focus. This helps show which is the element with the current focus when tabbing through the page.

#### Structural pseudo classes

* `li:first-child` selects only the first child li in a ul or ol.
* `li:last-child` conversely selects only the last child li in a ul or ol.
* `:only-child` selects elements which are the only children of their particular parent.
* `:nth-child(an + b)` selects the nth child of a parent element where b is the offset value, and a is the cycle multiple **after** the first element has been selected.

  * `odd` will select only odd elements, `even` will select only even elements
  * `3` will select only the 3rd element
  * `2n + 1` will select the 1st element (+ 1) followed by the 3rd element, 5th element etc
  * `3n` will select every 3rd element e.g. 3, 6, 9 etc
  * `-n+5` will select the 5th element, then 4th, 3rd, 2nd, 1st

* `:nth-last-child` is exactly the same, but starts from the bottom first

  * `-n+3` will here select the 3rd element from bottom, then the 2nd element from bottom and finally the last element i.e. the last 3 elements

* `:nth-of-type(an+b)` selects all sibling elements of the specified type
* `:nth-last-of-type(an+b)` is similar, but starts counting from the bottom
* `:only-of-type` selects elements if it is the only element of its type within its parent element

#### Additional pseudo classes
* `:root` will select the root element of the document (usually the html element). This may be useful since it has more specificity than the html element selector.
* `:target` can be used to style the target element of matching anchor. e.g. if `<a href="#s2">section 2</a>` targets a div with id s2, then when it is clicked, the string "#s2" is appended to the url and the browser uses this to style the element with matching id "#s2"
* `:empty` will select any empty elements. This may be useful for alerting the user to an empty result set, or an empty string
* `:not()` is the negation selector. e.g. `:not(:empty)` will select all elements which aren't empty; `:not([id="s1"])` will select all elements which don't have an id of "s1"

#### UI element states pseudo classes

* `:enabled` selects any form and input elements which are enabled e.g. `input[type="text"]:enabled`
* `:disabled` selects elements which are disabled
* `:checked` selects any form elements which are _checked_ e.g. check boxes and radio buttons. Radio button labels can be selected using a combination of this pseudo class with the adjacent sibling select e.g `input[type="radio"]:checked + label`. 

### Substring matching attribute selectors
#### Begins with ^=
* `a[href^="http://"]` selects any anchor elements with href attribute values beginning with "http://".
* `a[href^="mailto:]` selects all the anchor elements with email addresses.

#### Ends with $=
* `a[href$=".pdf"]` selects all anchor elements with an href attribute value ending with ".pdf".
* `a[href$=".doc"]` selects all anchor elements with an href attribute value ending with ".doc".

#### Contains
* `img[src*="thumb"]` selects all img elements with a src attribute value containing the string "thumb"

### Pseudo-elements

The difference between psuedo-elements and psuedo classes is that psuedo classes target actual elements, whereas psuedo-elements target virtual elements which don't always exist as elements.  
The two syntax variations `:first-letter` and `::first-letter` will both work, but the double colon is more common to distinguish that this is targeting a psuedo element.

* `::first-line` selects the first line
* `::first-letter` selects the first letter

Two further pseudo-elements allow inserting generated content.

* `::before` will insert the content before
* `::after` will insert the content after

Both require a `content` property which can specify the content to be inserted in a number of different ways: the actual content as a string; a url to an image; a reference to the content of an attribute on that element; or an empty string with extra css properties to e.g. draw a circle.

{% highlight css %}
.phone::before { content: "\2706"; /* common phone icon unicode */ }
.phone::before { content: url("img/phone.jpg"); }
.dload::before { content: attr(href); }
.dload::before { content: ""; height: 50px; width: 50px; display: inline-block; }
{% endhighlight %}

**Note** the generated contented is inserted into the actual element, rather than alongside.
