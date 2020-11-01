## Understanding Lexical Scope & Closures in JavaScript

### This post is a continuation of my other post [Javascript Scope rules](https://soumyadey.hashnode.dev/understanding-javascript-scope-rules-with-examples). If you haven't read it, check it out first.

<hr>

First, let me say that this blog post is highly inspired by the great JavaScript book [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/README.md), by [Kyle Simpson](https://github.com/getify).

>
I am assuming you have a good understanding of how JS scope rules work.

## Let's start
The first traditional phase of a standard language compiler is called tokenizing or, lexing. 

### What is Lexical Scope?
Lexical scope is a scope that is defined at the lexing time. In other words, lexical scope is based on where variables and blocks of scope are authored, by you, at write time.

Let's consider this block of code:
```
This example is taken from the book You Don't Know JS
```

```js
function foo(a) {

	var b = a * 2;

	function bar(c) {
		console.log( a, b, c );
	}

	bar(b * 3);
}

foo( 2 ); // 2 4 12
```
There are three nested scopes inherent in this code example

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/m0xyni56nkx79chu2ljb.png)

In the above code snippet, the Engine executes the `console.log(..)` statement and goes looking for the three referenced variables `a`, `b`, and `c`. It first starts with the innermost scope bubble, the scope of the `bar(..)` function. It won't find `a` there, so it goes up one level, out to the next nearest scope bubble, the scope of `foo(..)`. It finds `a` there, and so it uses that `a`. Same thing for `b`. But `c`, it does find inside of `bar(..)`.

Had there been a `c` both inside of `bar(..)` and inside of `foo(..)`, the `console.log(..)` statement would have found and used the one in `bar(..)`, never getting to the one in `foo(..)`.

Hence,
```
Scope look-up stops once it finds the first match.
```

**So in short, Lexical scope means that scope is defined by author-time decisions of where functions are declared. The lexing phase of compilation is essentially able to know where and how all identifiers are declared, and thus predict how they will be looked-up during execution.**

```
There are two mechanisms in JavaScript that can 
"cheat" lexical scope: `eval(..)` and `with`. 
We will talk about those in another post.
```

<hr>

Now that we have a solid understanding of scope, let's enlighten ourselves with an incredibly important part of the language: **Closures**

### So what are Closures?
Closures are not a special opt-in tool that you must learn new syntax and patterns for. Closures are all around in your javascript code. You just have to recognize and embrace it.

Let's take an example to fully understand closures once and for all.
```
This example is taken from the book You Don't Know JS
```
```js
function foo() {
	var a = 2;

	function bar() {
		console.log( a );
	}

	return bar;
}

var baz = foo();

baz(); // 2 -- Whoa, closure was just observed, man.
``` 

The function `bar()` has lexical scope access to the inner scope of `foo()`. But then, we take `bar()`, the function itself, and pass it *as* a value. In this case, we `return` the function object itself that `bar` references.

After we execute `foo()`, we assign the value it returned (our inner `bar()` function) to a variable called `baz`, and then we actually invoke `baz()`, which of course is invoking our inner function `bar()`, just by a different identifier reference.

`bar()` is executed, for sure. But in this case, it's executed *outside* of its declared lexical scope.

After `foo()` executed, normally we would expect that the entirety of the inner scope of `foo()` would go away, because we know that the *Engine* employs a *Garbage Collector* that comes along and frees up memory once it's no longer in use.

But the "magic" of **closures** does not let this happen. That inner scope is in fact *still* "in use", and thus does not go away.

By virtue of where it was declared, `bar()` has a lexical scope closure over that inner scope of `foo()`, which keeps that scope alive for `bar()` to reference at any later time.

**`bar()` still has a reference to that scope, and that reference is called closure.**

**Closure** lets the function continue to access the lexical scope it was defined in at author-time.

#### Closures are everywhere!
Let's see an example that shows that closures are really everywhere in Javascript

```js
function wait(message) {

	setTimeout( function timer(){
		console.log( message );
	}, 1000 );

}

wait( "Hello, closure!" );
```

We take an inner function (named `timer`) and pass it to `setTimeout(..)`. But `timer` has a scope closure over the scope of `wait(..)`, indeed keeping and using a reference to the variable `message`.

>
For more in-depth knowledge of Javascript Scopes and Closures be sure to have a read of the awesome book [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/README.md), by [Kyle Simpson](https://github.com/getify).

>
More in Closures:
- [Loops + Closures](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/scope%20%26%20closures/ch5.md#loops--closure)
- [Modules](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/scope%20%26%20closures/ch5.md#modules)

### Review
Closure seems to be like a mystical world set apart inside of JavaScript which only a few bravest souls can reach. But it's actually just a standard and almost obvious fact of how we write code in a lexically scoped environment, where functions are values and can be passed around at will.

<hr>

So, that's it. I hope you learned something new from this post. 
Show some love if you liked this post.

[Follow me on Github](https://github.com/Soumya-Dey).

[Follow me on Dev.to](https://dev.to/soumyadey)

#### And don't forget to comment your views about this post.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/e67sa6u0vueytg1kavpj.jpg)

Thanks for reading. 😄