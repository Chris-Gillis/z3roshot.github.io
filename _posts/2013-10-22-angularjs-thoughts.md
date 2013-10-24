---
layout: post
title: Learning AngularJS 
---

I'm building a new website in rails, and I decided to use AngularJS to make a single page application (SPA). A SPA is an application in which the page does not refresh between actions. Gmail is probably the most well known SPA. I don't think my app needs a SPA to be successful, but it makes for a really nice user experience. And I wanted to learn AngularJS.
So far I've had a couple problems that have slowed me down, and I wanted to document them here.

The first major hangup I had was breakage when using the browser's back and forward functions; when you used "back" the screen would flash the correct information for a moment and then it would go blank. Sometimes it would cause javascript errors, sometimes it wouldn't. I searched far and wide, and I just couldn't figure my problem out. In an attempt to do what many programmers have done, I posted [a question on stack overflow](http://stackoverflow.com/questions/19496453/angularjs-browser-back-button-stops-partials-from-loading-and-causes-page-refres). As you can read on the page, the problem was being caused by a feature that is turned on by default in Rails 4 called turbolinks. I didn't investigate exactly why this was happening, but then again I don't really care, I fixed my problem! Of course, credit where credit is due, my friend [red_square](twitter.com/red_square) diagnosed the problem for me. To remove turbolinks, I simply followed [these simple instructions](http://blog.steveklabnik.com/posts/2013-06-25-removing-turbolinks-from-rails-4).

My next major hangup I had was coffeescript related. I began programming my app in coffeescript, because that's the hip thing to do, plus the syntax is pretty nice. Since coffeescript is meant to be ruby-like, when it compiles to javascript, the last line of every function is prefixed with "return ". Normally this is no problem, but I was stuck for a long time because of this. When you're defining AngularJS controllers, you use the $scope object to add behaviors to your controller. In my code, the last line of the function was adding a behavior, so when it compiled to javascript it became
    return $scope.myFunc = function(...){...}
which Angular didn't like. I'm not sure exactly why this is a problem, but it was solved by returning undefined at the end of the function. It annoyed me enough that I decided to switch to plain javascript.

Since I solved those issues, it's been really smooth sailing. Even though it's a new way to think about creating a user interface, development is actually really quick once you move past the "gotchas". I'll definitely be posting more thoughts and musings about AngularJS, and I'll certainly talk more about my app when there is more to show.

