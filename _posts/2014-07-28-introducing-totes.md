---
layout: post
title: Totes, the chainable, extensible assertion framework for javascript
tags: [unit testing, javascript, totes]
---

![totes logo](https://camo.githubusercontent.com/3e83c3d59f1218e7c0fd90f0cdb9399ce3afed92/687474703a2f2f692e696d6775722e636f6d2f61516b6a7771522e706e67)

I wrote totes because I wanted to create an API that is easy to understand. I also wanted assertions that were chainable. At the core, totes has an `Assertable` object that has a `value` property and two functions: `isTrue` and `isFalse`. Everything else that totes can do is an extension on the `Assertable` prototype.

Totes is also easy to use. To get an instance of Assertable, you need to get a reference to the `expect` function and pass in a value that you want to make some assertions against: 
{% highlight javascript %}

var expect = require('totes').expect;

var assertable = expect('any value');

{% endhighlight %}

From there you can make any assertions you need to against the value you passed into `expect`:

{% highlight javascript %}

assertable.isTruthy();

assertable.isLetters();

assertable.yourNewCustomAssertion();

{% endhighlight %}

You can, as the title suggests, chain assertions because each assertion returns the `Assertable` object itself:

{% highlight javascript %}

assertable.isTruthy()
	.isLetters()
	.yourNewCustomAssertion();

{% endhighlight %}

There are many different types of assertions built onto assertable. To add more assertions you just need to extend the prototype of `Assertable`. To illustrate this, let's look at the `isZero` assertion.

{% highlight javascript %}
Assertable.prototype.isZero = function(){
	return this.isTrue(check, 'Failed isZero() assertion', {
		actual: this.value,
		expected: '0'
	});
	
	function check(val){
		return val === 0;
	}
};
{% endhighlight %}

Notice that the `isZero` function returns `this.isTrue(...)`. The first argument is a function that will take a value and produce a `true` value when the assertion passes. When the value returned is anything other than exactly `true` (including `"true"`), `isTrue` will throw an `AssertionError` which will be handled by the test runner. `isTrue` passes whatever value is passed into `expect` into the function argument. For example in this snippet:

{% highlight javascript %}
expect(0).isZero();
{% endhighlight %}

`isTrue` will pass `0` into the `check` function, which will return `true` because `0 === 0` is `true`.

In future blog posts I will talk more about the internals of Totes and give some real examples of it being used in real projects. I would love to hear from anyone using it to tell me about their experiences using it, and of course [I'm accepting pull requests](http://github.com/z3roshot/totes).
