## Understanding JavaScript Scope Rules

First , let me say that, this blog post is highly inspired from the great JavaScript book [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/README.md), by [Kyle Simpson](https://github.com/getify). 

After finishing the 1st title, I realized how I was only scratching the surface of JavaScript till now. It doesn't teach JavaScript as if you've never used it but it makes you realize how little you knew about the under-the-hood workings.

<hr>

### This post is about Scopes in JS, but I highly recommend you to give this book a try.
So let's get into the topic.

## What is scope actually?
Every programming language has a well-defined set of rules for storing variables in some location, and for finding those variables at a later time. We'll call that set of rules: Scope.

## Understanding Scope
The way we will approach learning about scope is to think of the process in terms of a conversation. But, *who* is having the conversation?

### The Cast

Let's meet the cast of characters that interact to process the program `var a = 2;`, so we understand their conversations that we'll listen in on shortly:

1. `Engine` : responsible for start-to-finish compilation and execution of our JavaScript program.

2. `Compiler` : one of *Engine*'s friends; handles all the dirty work of parsing and code-generation (see previous section).

3. `Scope` : another friend of *Engine*; collects and maintains a look-up list of all the declared identifiers (variables), and enforces a strict set of rules as to how these are accessible to currently executing code.

- When you see the program `var a = 2;`, you most likely think of that as one statement. But that's not how our new friend Engine sees it. In fact, Engine sees two distinct statements, one which Compiler will handle during compilation, and one which Engine will handle during execution.

### Compiler will proceed as : 
1. Encountering `var a`, Compiler asks Scope to see if a variable `a` already exists for that particular scope collection. If so, Compiler ignores this declaration and moves on. Otherwise, Compiler asks Scope to declare a new variable called `a` for that scope collection.

2. Compiler then produces code for Engine to later execute, to handle the `a = 2` assignment. The code Engine runs will first ask Scope if there is a variable called `a` accessible in the current scope collection. If so, Engine uses that variable. If not, Engine looks elsewhere (see nested Scope section below).

3. If Engine eventually finds a variable, it assigns the value `2` to it. If not, Engine will raise its hand and yell out an error!

#### Before proceeding further let us know about 2 important terms.
- **LHS** : It means that the Engine would be performing an look-up for a variable.
- **RHS** : It means "retrieve his/her source (value)", implying that RHS means "go get the value of...".

## Engine/Scope Conversation
```
This example is taken from the book You Don't Know JS
```

```js
function foo(a) {
	console.log( a ); // 2
}

foo( 2 );
```

Let's imagine the above exchange (which processes this code snippet) as a conversation. The conversation would go a little something like this:

- ***Engine***: Hey *Scope*, I have an RHS reference for `foo`. Ever heard of it?

- ***Scope***: Why yes, I have. *Compiler* declared it just a second ago. He's a function. Here you go.

- ***Engine***: Great, thanks! OK, I'm executing `foo`.

- ***Engine***: Hey, *Scope*, I've got an LHS reference for `a`, ever heard of it?

- ***Scope***: Why yes, I have. *Compiler* declared it as a formal parameter to `foo` just recently. Here you go.

- ***Engine***: Helpful as always, *Scope*. Thanks again. Now, time to assign `2` to `a`.

- ***Engine***: Hey, *Scope*, sorry to bother you again. I need an RHS look-up for `console`. Ever heard of it?

- ***Scope***: No problem, *Engine*, this is what I do all day. Yes, I've got `console`. He's built-in. Here ya go.

- ***Engine***: Perfect. Looking up `log(..)`. OK, great, it's a function.

- ***Engine***: Yo, *Scope*. Can you help me out with an RHS reference to `a`. I think I remember it, but just want to double-check.

- ***Scope***: You're right, *Engine*. Same guy, hasn't changed. Here ya go.

- ***Engine***: Cool. Passing the value of `a`, which is `2`, into `log(..)`.

- ...

## Nested Scope
Just like we can have nested blocks of code, we can also have nested scope i.e. one or more scopes nested inside another scope.
So when a variable couldn't be found in a scope, the Engine consults the immediate outer scope, and continuing until it reaches the global scope. 

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/utrxj6pm6j75ap7e47zx.png)

```
Another great example from the book
```

```js
function foo(a) {
	console.log( a + b );
}

var b = 2;

foo( 2 ); // 4
```

The RHS reference for `b` cannot be resolved inside the function `foo`, but it can be resolved in the *Scope* surrounding it (in this case, the global).

So, revisiting the conversations between *Engine* and *Scope*, we'd overhear:

> ***Engine***: "Hey, *Scope* of `foo`, ever heard of `b`? Got an RHS reference for it."

> ***Scope***: "Nope, never heard of it. Go fish."

> ***Engine***: "Hey, *Scope* outside of `foo`, oh you're the global *Scope*, ok cool. Ever heard of `b`? Got an RHS reference for it."

> ***Scope***: "Yep, sure have. Here ya go."

The simple rules for traversing nested *Scope*: *Engine* starts at the currently executing *Scope*, looks for the variable there, then if not found, keeps going up one level, and so on. If the outermost global scope is reached, the search stops, whether it finds the variable or not.

## Errors
- If an RHS look-up fails to ever find a variable, anywhere in the nested *Scope*s, this results in a `ReferenceError` being thrown by the *Engine*. It's important to note that the error is of the type `ReferenceError`.

- By contrast, if the *Engine* is performing an LHS look-up and arrives at the top floor (global *Scope*) without finding it, and if the program is not running in [Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode), then the global *Scope* will create a new variable of that name **in the global scope**, and hand it back to *Engine*.

*"No, there wasn't one before, but I was helpful and created one for you."*

- Now, if a variable is found for an RHS look-up, but you try to do something with its value that is impossible, such as trying to execute-as-function a non-function value, or reference a property on a `null` or `undefined` value, then *Engine* throws a different kind of error, called a `TypeError`.

`ReferenceError` is *Scope* resolution-failure related, whereas `TypeError` implies that *Scope* resolution was successful, but that there was an illegal/impossible action attempted against the result.

<hr>

So, that's it. I hope you learned something from this post. 
Show some love if you liked this post. [Follow me on Github](https://github.com/Soumya-Dey).

### And don't forget to comment your views about this post.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/e67sa6u0vueytg1kavpj.jpg)

Thanks for reading. 😄