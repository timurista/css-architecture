# CSS Architecture

A high level view of the common css approaches. This work was inspired by the book Enduring CSS by ben Frian.

## Specificty Problem for large scale applications
As developers we are often faced with the challenge of trying to design our system in a way which is easy to read and reason about. The cascading nature of css can create a number of headaches because of how specificty is assigned. The different problems outlined below attempt to solve the specificty issue through a conscious design of the css naming convention.

The goal currently for css rules is this:
> making sure specificity ...homogeneous across rules

## Limitations of IDs as selectors
> In summary, they are far more specific than a class selector - therefore making overrides more difficult. Plus they can only be used once in the page anyway so their efficacy is limited.

However, to keep specificty lower you can do the following: 
```css
[id="Thing"] {
/* Property/Values Here */
}
```

## Object Oriented CSS 

The best exmple of this approach is [Atomic CSS](https://acss.io/) where the class name is composed of different features which make up or compose the overall styling. The philosophy behind atomic css is to break the css into a variety of building blocks which can be declared inside the element. In this way, the component retains control of the styling, and the user can create variables and customize the stylistic building blocks for the application.

Here is on example:
```html
    <div class="Bgc(#0280ae.5) C(#fff) P(20px)">A big callout section</div>
```
In this case, Bgc would be background color and the element inside the () is the value for that background color. Taking this one step further, you could even write `Bgc(grey-color)` and abstract the grey-color into a variable which can be used throughout your application.

Using the shorthand nomenclature for Atomic css, the grid system can be vastly shortened. Here is an example of an atomic css grid system for inline blocks:
```html
<div>
   <div class="IbBox W(1/3) P(20px) Bgc(#0280ae.5)">Box 1</div>
    <div class="IbBox W(1/3) P(20px) Bgc(#0280ae.8)">Box 2</div>
    <div class="IbBox W(1/3) P(20px) Bgc(#0280ae">Box 3</div>
</div>
```
Above, the IbBox determines the type to be an inline-block, the width is 1/3, P(20px) = padding 20px, and Bgc is background color and the .5 is opacity 50%.

### Pros
* Variables can be passed along in a more intuitive manner, closer to the DOM structure.
* Grid system is more obvious than a standard bootstrap row approach which abstracts the underlying CSS.
* Is more composable and reduces the effort needed to override using stylesheets

### Cons
* Responsive Web design is still a pain because you need to add a media breakpoint name to an atomic class in order to apply specific styling. So you end up with something like this:

```html
   <div class="D(ib)--sm W(50%)--sm W(25%)--lg P(20px) Bgc(#0280ae.5)">1</div>
   <div class="D(ib)--sm W(50%)--sm W(25%)--lg P(20px) Bgc(#0280ae.6)">2</div>
   <div class="D(ib)--sm W(50%)--sm W(25%)--lg P(20px) Bgc(#0280ae.8)">3</div>
   <div class="D(ib)--sm W(50%)--sm W(25%)--lg P(20px) Bgc(#0280ae)">4</div>
```
(In which case it is almost better to use media querieis in css style sheets.)

* sometimes you really don't want this level of detail when composing an element, but a more general component style will suffice such as `label`

## Scalable Modular CSS

The idea behind this approach is really to organize your code or group the css into flexible elements which also promote long term maintainability. [SMCSS](https://smacss.com/book/) uses the following categorizations for css:
- Base
- Layout
- Module
- State
- Theme

### Why Categorize?
The idea here is to codify patterns, which can lead to resuable code. The SMCSS approach is fairly agnostic to any particular class naming convetion, however they do recommend that the different categorizies be condensed and used as prefixes for your styles. For example, one might use layout-row-2 or l-row-2 for a layout style. However, when it comes to modules and components it makese more sense to use the name of the component itself. 

## BEM Naming Convention

Block Element Modifier or (BEM) is an approach to naming css classes in order to bypass the specificity problem and overriding hell in CSS. 
```cs
.site-search {} /* Block */
.site-search__field {} /* Element */
.site-search--full {} /* Modifier */
```

### Pros
* Easy naming system

## Cons
* Modifiers can be confusing -- does it change state? Does it reflect a component attribute?

## BEM naming enhancements aka BEMIT
Hungarian Notation, you can use c-, for Components, o-, for Objects, u-, for Utilities, and is-/has- for States (there are plenty more detailed in the linked post).

[Responsive suffixes](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/) using @ breakpoint.

```html
<div class="o-media@md  c-user  c-user--premium">
  <img src="" alt="" class="o-media__img@md  c-user__photo  c-avatar" />
  <p class="o-media__body@md  c-user__bio">...</p>
</div>
```

```css
@media print {
  /* you must escape the @ character */
  .u-hidden\@print { 
    display: none;
  }

}
```

## Enduring CSS
Takes a lot from BEM styling but 


**The ten commandments of Enduring CSS**
1. Thou shalt have a single source of truth for all key selectors
2. Thou shalt not nest, unless thou art nesting media queries or overrides
3. Thou shalt not use ID selectors, even if thou thinkest thou hast to
4. Thou shalt not write vendor prefixes in the authoring style sheets
5. Thou shalt use variables for sizing, colours and z-index
6. Thou shalt always write rules mobile first (avoid max-width)
7. Use mixins sparingly, and avoid @extend
8. Thou shalt comment all magic numbers and browser hacks
9. Thou shalt not inline images
10. Thou shalt not write complicated CSS when simple CSS will work just as well

## Extra resources
[Compare Selector Speed](https://benfrain.com/selector-test/)