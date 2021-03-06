---
layout: post
title:  "Angular - Directives"
date:   2019-09-11 16:45:22 +0100
categories: webdev angular
---

Directives
========================

## What is a directive?

A directive is a class that has control over a section of the DOM or can modify the component data model. A directive most commonly has an associated HTML element or attribute, which can be referred to as the directive itself.
## Structural Directives
### What is a structural directive?

A structural directive is a directive that changes or controls the DOM *layout*. They can do this by adding, removing or otherwise manipulating DOM elements.

### How do you use a structural directive?

Any structural directive is preceded with an asterisk (*), for example:

`<p *ngFor="let item of list"> {{item.title}}</p>`

This takes a variable called `list`, and iterates through each element, adding a `<p>` element to the page with the innerHTML being the `title` property of the item.

### What are the built-in structural directives?

The most common structural directives are `ngFor`, `ngIf` and `ngSwitch`. `ngFor` is described above, while `ngIf` is a simple if-statement, e.g.:

`<p *ngIf="contentIsShowing" > Content </p>`

will only render "Content" if the `contentIsShowing` expression evaluates to true.

`ngSwitch` is a switch-case directive:

```
<div [ngSwitch]="color">
	<p *ngSwitchCase="red"> The item is red </p>
	<p *ngSwitchCase="blue"> The item is blue </p>
	<p *ngSwitchCase="green"> The item is green </p>
	<p *ngSwitchDefault> The item is neither red, green, or blue </p>
</div>
```
Although the above example could probably be more easily programmed with `*ngIf` directives.

## Attribute Directives

### What is an attribute directive?

An attribute directive is simply a directive that changes the appearance or behavior of a DOM element.

### How do you use an attribute directive?

`<p appHighlight > Hover this text </p>`

Note that while the directive has been declared, it must first be created. Running `ng generate directive highlight` will produce the appropriate file, and add declares the directive in the root AppModule.

Now to specify what the directive *does*:

```
@Directive({
	selector: '[appHighlight]'
})
export class HighlightDirective {
	constructor(element: ElementRef) { 
		element.nativeElement.style.backgroundColor = 'blue';
	}
}
```
(Note the use of square brackets in `[appHighlight]`, this specifies that this is a CSS attribute selector.)
We now have a directive that selects any elements that match the given CSS attribute selector query, and then takes the element and changes their background colour style attribute to 'blue'.

### Making attribute directives do work

With the above code, we might as well have just specified the highlight colour in our stylesheet. If we want to change the page *dynamically*, we can use the `HostListener` decorator to listen for DOM events, and react to them:

```
@HostListener('mouseenter') onMouseEnter(){
	this.highlight('blue')
	}
	
@HostListener('mouseleave') onMouseLeave(){
	this.highlight(null)
}

private highlight(string: colour){
	this.element.nativeElement.style.backgroundColor = colour;
}
```
