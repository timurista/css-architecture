# CSS Architecture

A high level view of the common css approaches. This work was inspired by the book Enduring CSS by ben Frian.

## Specificty Problem for large scale applications
As developers we are often faced with the challenge of trying to design our system in a way which is easy to read and reason about. The cascading nature of css can create a number of headaches because of how specificty is assigned. The different problems outlined below attempt to solve the specificty issue through a conscious design of the css naming convention.

The goal currently for css rules is this:
> making sure specificity ...homogeneous across rules

## Why?

## Object Oriented CSS 

The best exmple of this approach is Atomic CSS where the class name is composed of different features which make up or compose the overall styling.

```html
    <div class="Bgc(#0280ae.5) C(#fff) P(20px)">A big callout section</div>
```

[Atomic CSS](https://acss.io/) is a prime example of this approach. The philosophy behind atomic css is to break the css into a variety of building blocks which can be declared inside the element. In this way, the component retains control of the styling.

## Atomizer
To deal with responsive web design issues, the atomizer is a package which can generate your different blocks for you and convert your css for large scale application.


| Pros | Cons |
| --- | --- |
| good for you | breaks down in responsive queries |

### When to use?


## Scalable Modular CSS

## BEM Naming Convention

## Enduring CSS


