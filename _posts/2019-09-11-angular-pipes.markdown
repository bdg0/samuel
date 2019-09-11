---
layout: post
title:  "Angular - Pipes"
date:   2019-09-11 16:42:22 +0100
categories: webdev angular
---

Pipes
========================

## What are pipes?

Pipes are a way of **transforming** input data into the display format you want.

## What does using a pipe look like?

In the [Angular core library](https://angular.io/api/core), there exists a few in-built pipes.

To use a pipe, you simply flow the input data through the pipe operator into a pipe function inside the interpolation expression:

`<p> Your name is {{name | lowercase}} <p>`

This takes the `name` variable, and puts it through the `lowercase` built-in pipe function before displaying it. 

Note that pipes can be chained by just continuing to pipe the return value into the next pipe function.

## How do you make your own pipe functions?

Using the `@Pipe`  decorator, and implementing the `PipeTransform` interface:

```
@Pipe({name: 'isNumber'})
export class IsNumberPipe implements PipeTransform {
 transform(value: any): string{
	 return isNan(value) ? 'not a number' : 'a number';
 	}
};
```

When a pipe function is called, Angular will call the `transform` method.

## How do you use your own pipe functions?

Once you've included the pipe in the declarations array of the AppModule, you can use it just like a built-in.

```
@Component({
	selector:'numberInput',
	template:'<p> Your input is {{input | isNumber}} </p>'
});
export class NumberInputComponent { }
```
