---
layout: post
title: My First Real Experience With BDD
---

I've subscribed to behavior driven development for a long time now. I use the
word subscribe here to mean I read about it, and I talk about it, but I haven't
yet implemented it on any of my projects. Well I decided to actually give it a
shot on a project I started recently, and it's even better than I expected it to
be!

###User Stories - The Beginning

With BDD you have a different focus than traditional software design. You begin
with [user
stories](http://en.wikipedia.org/wiki/User_story), and you write software
to satisfy each story. The name of this section is a slight misnomer. This will often be the beginning for engineers, but it isn't the beginning of the process. User stories are written to satisfy features or requirements for the software.
Here is an example of a user story I wrote for my new project.

~~~~~
User should be able to select a restaurant from a list of restaurants.
~~~~~

###Driving Development with Testing

This project is a rails project, and I am using both [Cucumber](http://cukes.info) and
[RSpec](http://rspec.info) for testing. Cucumber is more relevant because it lets you
define behaviors that you're going to test. Here is the behavior I wrote for
that story.

~~~~~
Given A restaurant exists and it has a list of menu items
When I go to the restaurant list page
And I select the restaurant
Then I should be on the menu page
And I should see the name of the restaurant
~~~~~

The way behavior driven development works is that you write these features first,
before any code. Since there is no code, you're going to get some failures, all
the failures. The goal is to write just enough code to pass the tests. Because
you only write code to pass the tests, your code because laser focused and only
relevant to the specific features you're solving. It's incredibly easy to write
a feature and 30 of it's closest feature friends and not use most of them. Not
only is this a waste of time, it makes the code noisy and difficult to read
later.

I feel this technique has improved my game a lot. As I mentioned, this is a
rails project, and if you've used rails you know that it has a tendency to
generate a lot of things you don't necessarily need. This approach gives me the
tools I need to fight back against unnecessary code, and so far it's pretty
wonderful.
